# DietNetworks: Thin parameters for Fat Genomics

This repo contains the code to reproduce the experiments of the paper [DietNetworks: Thin parameters for fat genomics](https://arxiv.org/abs/1611.09340).

## Before you start

- Download and install Theano and Lasagne.
- Download the 1000 Genomes dataset as described in appendix B of the paper.

## Generate the pre-computed embeddings if necessary

## Run Experiments

### Diet Networks with per class histograms (fold 0)

cd experiments/variant2

Experiments without reconstruction loss:

THEANO_FLAGS='device=gpu' python learn_model.py --embedding_source=/path/to/per_class_histograms/fold0.npy --which_fold=0 -exp_name='dietnets_' -embedding_input='histo3x26' --learning_rate=0.0001 -eni=0.01 -dni=0.01 -l=0 -g=0

Experiments with reconstruction loss:

THEANO_FLAGS='device=gpu' python learn_model.py --embedding_source=/path/to/per_class_histograms/fold0.npy --which_fold=0 -exp_name='dietnets_' -embedding_input='histo3x26' --learning_rate=0.0001 -eni=0.01 -dni=0.01 -l=0 -g=10


### Parameters in experiments/variant2/learn_model.py
- dataset: Str. Dataset name. (default: '1000_genomes').
- n_hidden_u: List. Considering the Emb. of Fig. 1 (b)/(c) an MLP -> number of hidden units of each layer of the MLP. The parameters of the embedding are shared among auxiliary networks in Fig. 1 (b) and (c). **Set to [100] for DietNetworks experiments, ignored when a particuler embedding is required.**
- n_hidden_t: List. Number of hidden units of the MLP depicted in Fig. 1 (b)/(c). Both MLP have the same structure (number of layers, number of hidden units per layer) but do not share parameters. **Set to [100] for DietNetworks experiments.**
- n_hidden_s: List. Number of hidden units of the second MLP in Fig. 1 (a). **Set to [100] for DietNetworks experiments.**
- embedding_source: Str. Path to the .npy file where the mebedding to be used in the Diet Networks framework is saved.
- num_epochs: Int. Maximum number of epochs. **Set to 500 for DietNetworks experiments.**
- learning_rate: Float. Learning rate. (default: 0.0001)
- learning_rate_annealing: Float. Learning rate annealing. (default: 0.99)
- alpha: Float. **Set to 0 for all experiments.**
- beta: Float. **Set to 0 for all experiments.**
- gamma: Float. **Set to 0 if no reconstruction loss, set to 10 otherwise.**
- lmd: Float. Weight decay. **Set to 0 for all Diet Networks experiments.**
- disc_nonlinearity: Str. Nonlinearity to be used at the top layer of Fig. 1 (a). (default: softmax)
- encoder_net_init/decoder_net_init: Float. Initialization values. (default 0.01)
- keep_labels: Float. **Set to 1.0 for all experiments.**
- prec_recall_cutoff. Int. **Set to 0 for all experiments.**
- which_fold: Int. Which fold to use.
- early_stop_criterion: Str. **Set to accuracy for all experiments.**
- embedding_input: The kind of embedding to be used in the auxiliary networks (histo3x28 for per class histogram, bin for snp2vec, raw for no pre-computed embedding).
- save_tmp: Str. Where to temporarily save the training curves and models (used during training, can be the same as save_perm).
- save_perm: Str. Where to save the final results (used at the end of the training, can be the same a save_tmp).
- dataset_path: Str. Path to dataset.
- resume: Bool. In case we need to resume the training.
- exp_name: Str. If we want a particular experiment name to be concatenated at the beginning of the generated name. (default: '')
- random_proj: Int. Whether we want to use random projections as embedding. (default: 0)

