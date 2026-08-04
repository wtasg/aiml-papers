# Fine-Tuning

Fine-tuning is the process of continuing the training of a pre-trained model on a task-specific dataset by updating its weights.

The key idea is:

> Adapt a pre-trained model to a new task by updating all of its trainable weights.

## Idea behind Fine-Tuning

A pre-trained model already understands general language and patterns. Fine-tuning specializes it for a downstream task by training it on labeled task-specific examples.

Unlike [LoRA](/answers/lora.md), every trainable weight in the model is updated.

Training follows this loop:

1. Forward pass: `ŷ = f(x)`
2. Compute the loss: `L = Loss(ŷ, y)`
3. Backpropagate the gradients.
4. Update the weights.
5. Repeat until convergence.

## Maths behind Fine-Tuning

1. Let the pre-trained weight matrix be:

   `W ∈ ℝ^(d×k)`

2. For an input `x`, the forward pass is:

   `h = Wx`

3. Compute the loss:

   `L = Loss(ŷ, y)`

4. Compute the gradient:

   `∂L/∂W`

5. Update the weights:

   `W ← W − η(∂L/∂W)`

   where `η` is the learning rate.

6. Repeat over many batches and epochs to obtain the fine-tuned weights `W'`.

7. During inference:

   `h = W'x`

## Training Pipeline

- Pre-trained Model
- Task-specific Dataset
- Forward Pass
- Loss Computation
- Backpropagation
- Weight Update
- Repeat

## Advantages

- Highest adaptation capacity.
- Every parameter can specialize for the task.
- No architectural changes are required.

## Disadvantages

- High memory and compute requirements.
- Large optimizer state.
- Produces a full copy of the model.
- Can suffer from catastrophic forgetting.

## Fine-Tuning vs LoRA

| Fine-Tuning | LoRA |
| - | - |
| Updates all trainable weights | Updates only low-rank adapters |
| High memory usage | Low memory usage |
| Produces a full model | Produces a small adapter |
| Higher adaptation capacity | Lower adaptation capacity, but much cheaper |
