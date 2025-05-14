# AI Music Recommender

## Abstract  
An AI-powered music recommendation system was developed to capture and reflect individual listening preferences by focusing on musical characteristics—such as rhythm, energy, and mood—rather than genre or popularity. A hybrid model combines a neural collaborative filtering network trained on user–track interaction data with a content-based fallback that uses cosine similarity over audio features, achieving a test RMSE of 0.1785 on held-out ratings. 

## Introduction  
Traditional music recommenders rely heavily on genre tags or collaborative filtering, which can miss the underlying audio qualities that define a listener’s taste. This project leverages Spotify’s dataset of over 360,000 tracks with 19 audio features to build a system that learns latent user–track patterns via embeddings, while also enabling cold-start recommendations through feature similarity.

## Data Collection & Feature Engineering  
Track data were sourced from Spotify’s Web API, yielding more than 150,000 unique records with 13 raw audio metrics (danceability, energy, loudness, etc.). Seven additional features—such as “dance valence,” “mood score,” and “dance intensity”—were engineered to capture higher-order listener cues. The dataset was cleaned (duplicates and outliers removed), null entries filtered, and all numeric fields min–max scaled to [0,1]. 

## Methods  
A hybrid framework was implemented:  
- **Neural Collaborative Filtering:** A feedforward network uses a 50-dimensional embedding layer for track IDs, followed by two dense layers (64 and 32 units) with ReLU activations, dropout (0.2), and a linear output predicting user enjoyment. Trained with Adam (LR=0.001) and early stopping.  
- **Content-Based Fallback:** User profiles average engineered feature vectors of liked tracks; cold-start recommendations are ranked by cosine similarity to this profile. 

## Autoencoder Architecture  
An autoencoder compresses 16 audio features into a 32-dimensional latent space and reconstructs them through a mirrored decoder. Both encoder and decoder use a dense layer (64 units), batch normalization, ReLU activation, and 0.3 dropout. The model minimized MSE, achieving validation RMSE of 0.134 and test RMSE of 0.0375. 

## Experiments & Results  
Data were split into training (120k), validation (15k), and testing (15k). The final autoencoder achieved test RMSE of 0.1004, outperforming three baselines (random RMSE 0.23, popularity-based RMSE 0.15, content-based RMSE 0.138). Key predictors included mood score, energy–loudness, and dance intensity.

## Use Cases  
- **Cold-Start Track Placement:** Simulated for a new Jason Mraz release, positioning it alongside stylistically similar artists.  
- **Personalized Discovery:** For user “RAF,” the system returned indie folk and soft-rock tracks matching low-tempo, high-acoustic preferences without relying on popularity.

## Conclusion & Future Work  
The hybrid recommender delivers accurate, interpretable, and cold-start-resilient suggestions. Future enhancements include incorporating lyrics embeddings, temporal listening context, live feedback loops, and graph-based co-occurrence models to further enrich personalization. 
