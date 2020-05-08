# Experiment results of testing with LSTM and hidden states 


## The following are different versions of passing hidden states:

0. `lstm`: no hidden states passed and updated between action taking steps as well as batches of training
  * >1 layers of lstm has better performance than original nn in terms of convergence speed and stability
  * 1 layer of lstm performs worse than original nn

1. `lstm-pass-hidden-in-episode`: hidden states passed and updated between action taking steps
  * failing to converge when number of layers > 1
  * 1 layer of lstm performs a little worse than version 0

2. `lstm-hidden`: hidden states saved between steps with the corresponding step's states and action, and fed as hidden input of batch training (*BUGGY*: mismatch between states, action of the current step and hidden states output for next step)
  * failing to converge in 1 layer case
  * >2 layers of lstm performs a little worse than version 0

3. `lstm-hidden-matched`: after fixing the bug in version 2
  * slightly better than version 2 when numer of layers >1
  * 1 layer of lstm can converge though suffers more fluctuation than version 0

4. `lstm-hidden-matched-both`: combing version 1 and version 3
  * better than all previous versions
