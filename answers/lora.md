# Low-Rank Adaptation LoRA

LoRA (Low-Rank Adaptation) is a parameter-efficient fine-tuning (PEFT) technique that adapts a pre-trained neural network by freezing the original weights and learning a small set of additional low-rank matrices instead of updating the full model.

The key idea is:

> Most task-specific changes to a large model can be approximated by a low-rank update to its weight matrices.

This dramatically reduces the number of trainable parameters, memory usage, and storage requirements.

## Idea behind LoRA

Updating the entire pre-trained weight matrix `W` during fine-tuning is expensive.

LoRA freezes `W` and learns only the weight update `∆W`. Instead of learning the full `∆W`, it approximates it as the product of two much smaller matrices: `∆W = BA`, where the rank `r` is chosen such that: `r << min(d, k)`

Since `A` and `B` contain far fewer parameters than `W`, training requires significantly less memory and computation.

For an input `x`, the forward pass is:

1. Original model: `Wx`
2. LoRA update: `BAx`
3. Final output: `(W + BA)x = Wx + BAx`

You can think of the LoRA branch as a small correction that is added to the output of the frozen pre-trained model.

## Maths behind LoRA

1. Let the pre-trained weight matrix be `W ∈ ℝ^(d×k)`.

2. For an input `x`, the standard forward pass is:

   `h = Wx`

3. During fine-tuning, the original weight matrix `W` is frozen. Instead of learning a full weight update, LoRA assumes the adaptation `∆W` is **low-rank**.

4. The adaptation is factorized as:

   `∆W = BA`

   where:

   - `B ∈ ℝ^(d×r)`
   - `A ∈ ℝ^(r×k)`

   so that `BA ∈ ℝ^(d×k)`.

5. The rank `r` is chosen to be much smaller than the dimensions of `W`:

   `r << min(d, k)`

6. The forward pass with LoRA becomes:

   `h = (W + ∆W)x = Wx + BAx`

7. At initialization:
   - `A` is initialized with small random (typically Gaussian) values.
   - `B` is initialized to all zeros.

   Therefore, initially:

   `∆W = BA = 0`

   and the model behaves identically to the original pre-trained model.

8. The LoRA update is scaled by:

   `α / r`

   giving the final forward pass:

   `h = Wx + (α/r)BAx`

   where `α` (alpha) is a constant hyperparameter controlling the strength of the adaptation.

9. Number of trainable parameters:

   - Full fine-tuning: `d × k`
   - LoRA: `(d × r) + (r × k) = r(d + k)`

10. During inference, the learned update can be merged into the original weights:

    `W' = W + (α/r)BA`

    After merging, the layer behaves exactly like a standard linear layer with no additional inference overhead.
