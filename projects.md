---
layout: page
title: Projects
permalink: /projects/
---

<div class="image-wrapper left-image" style="text-align: center;">
  <img src="https://danhlv.github.io/static/img/dan_left.png" alt="The flow field around an omni-directional wind turbine" style="width: 65%; display: block; margin: 0 auto;">
</div>



Here are some of my recent and ongoing projects:

###  [Generative AI–driven development of airfoil geometries optimized for aerodynamic performance. ](https://danhlv.github.io/AIgeneratedairfoils/)

We want to create a pipeline that will generate new NACA airfoils geometries. These newly AI-generated geometries that will have the aerodynamic performance of our choice in terms of forces and pressure distribution for given angles of attack and Reynolds numbers.
- We want to train an autoencoder on airfoil geometries to capture the distribution of shapes in a latent space.
-  Then we want to train an inverse neural network that will map the aerodynamic performance of the NACA airfoils onto their respective latent geometries.
- We then generate our ideal set of performance parameters and pass them through the inverse NN which will yield a new latent space geometry that will be translated back to original euclidian geometry space by the decoder of the autoencoder. Ideally this NACA computer-generated airfoil will have the performance that we thought about initially.

###  [Naïve Bayes classifier](https://danhlv.github.io/naivebayes/)

A Naïve Bayes classification approach based on Maximum Likelihood Estimation (MLE) of class-conditional densities
- MLE to fit probabilistic models
- Bayes' rule
- multivariate normal distribution

###  Design optimization for Wind Turbine Shrouds
- Integrated neural networks with CFD simulations for adaptive geometry control.
- Enabled performance optimization through simulation-informed machine learning.

###  AI-Based Pitch Control System
- Used neural networks to adapt the pitch of the blades to incoming wind conditions.
- Maintaining optimal rotational speed

###  Engine control Unit
- Developed AI algorithm that governs the functioning of a generator engine.

###  Neo4j + Kafka Kubernetes Pipeline
- Built a data ingestion pipeline with Kafka Connect and Neo4j.
- Used in large-scale graph analysis of NYC taxi data.

###  My RAG (Retrieval-Augmented Generation)

A RAG system that answers questions based on a local set of documents using:
- SentenceTransformers for embeddings
- FAISS for retrieval
- OpenAI GPT-4 for generation





*More coming soon...*



<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-M9GDRMZKXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-M9GDRMZKXX');
</script>
