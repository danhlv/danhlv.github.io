---
layout: page
title: "AeroML: Generative AI–driven development of airfoil geometries optimized for aerodynamic performance."
permalink: /AIgeneratedairfoils/
---

This project develops a computational pipeline for the generation of novel NACA airfoil geometries using artificial intelligence. The pipeline is designed to synthesize new airfoil shapes that meet prescribed aerodynamic performance targets, including force coefficients and pressure distributions, for specified angles of attack and Reynolds numbers. By coupling geometry generation with aerodynamic performance constraints, the framework enables the systematic design of airfoils tailored to user-defined operating conditions.

### Workflow Summary

#### 1️⃣ Data Loading

For this project, we use the **AirfRANS** dataset, available here:  
<a href="https://airfrans.readthedocs.io/en/latest/" target="_blank" rel="noopener noreferrer">https://airfrans.readthedocs.io</a>

The dataset is extracted from CFD simulations in two steps:

- **Step 1:** Extract the NACA airfoil contours (pairs of points $(x, y)$) together with the corresponding pressure distribution.  
- **Step 2:** Extract the aerodynamic performance quantities — lift $(C_L)$, drag $(C_D)$, moment coefficients $(C_M)$, forces, angle of attack $(AoA)$, and Reynolds number$(Re)$.

---

#### 2️⃣ Build and Train the Autoencoder (Using CST Coefficients)

Instead of raw $(x,y)$ coordinates, each airfoil is represented using **CST (Class–Shape Transformation) coefficients**:

- Upper surface: $N_{\text{CST}} + 1 = 9$ coefficients  
- Lower surface: $9$ coefficients  

<figure style="text-align: center;">
  <img src="https://danhlv.github.io/static/img/autoencoder_template.png"
       alt="Fig.1 - The autoencoder used"
       style="width: 80%; display: block; margin: 0 auto;">
  <figcaption style="font-size: 14px; margin-top: 8px;">Fig.1 - The autoencoder used</figcaption>
</figure>

**Total input dimension:**
$$
18\ \text{CST coefficients per airfoil}
$$

By using CST coefficients and a compressed latent space, the inverse network learns how to generate **realistic airfoils** that match target aerodynamic properties, while the decoder ensures the output stays on the manifold of **valid and smooth** airfoil geometries.

These 18 parameters go into the autoencoder.

**Encoder:**  
Compresses the CST coefficients into a low-dimensional latent vector $z$:
$$
z = f_{\text{enc}}(\text{CST}_{18})
$$

**Decoder:**  
Reconstructs the CST coefficients from the latent code:
$$
\widehat{\text{CST}} = f_{\text{dec}}(z)
$$

This builds a **latent manifold of valid airfoil shapes**.

---

#### 3️⃣ Build and Train the Inverse Network

Once the autoencoder is fully trained and **frozen**, a second network is trained:

$$
\left[\, F_{\text{tot}X},\ F_{\text{tot}Y},\ C_D,\ C_L,\ C_M,\ Re,\ AoA,\ p_{\text{distribution}}\,\right]
\;\xrightarrow{\,f_{\text{inv}}\,}\;
z
$$

This inverse model learns how aerodynamic targets map to appropriate latent codes.

---

#### 4️⃣ Create a New Aerodynamic Target Vector

You choose a desired performance vector, for example:
$$
\left[\, F_{\text{tot}X}^{\ast},\ F_{\text{tot}Y}^{\ast},\ C_D^{\ast},\ C_L^{\ast},\ C_M^{\ast},\ Re,\ AoA,\ p_{\text{distribution}}^{\ast}\,\right]
$$

---

#### 5️⃣ Pass the Target Through the Inverse Network

The inverse model outputs a latent vector:
$$
z^{\ast} = f_{\text{inv}}(\left[\, F_{\text{tot}X}^{\ast},\ F_{\text{tot}Y}^{\ast},\ C_D^{\ast},\ C_L^{\ast},\ C_M^{\ast},\ Re,\ AoA,\ p_{\text{distribution}}^{\ast}\,\right])
$$

---

#### 6️⃣ Decode the Latent Code into CST Coefficients

Using the decoder:
$$
\widehat{\text{CST}}^{\ast} = f_{\text{dec}}(z^{\ast})
$$

These CST coefficients represent a new, AI-generated airfoil shape.

---

#### 7️⃣ Reconstruct and Plot the New Airfoil

Use the CST reconstruction formula to map the coefficients back to smooth $(x,y)$ coordinates, plot the geometry, and analyze the resulting shape.
