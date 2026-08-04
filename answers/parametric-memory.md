# Parametric memory

Parametric memory is the knowledge stored inside the model's parameters (weights) after training.

When an LLM is trained, gradient descent adjusts billions of weights. Those weights collectively encode statistical patterns about language, facts, reasoning, syntax, and world knowledge.

Changing parametric memory requires:

+ Pretraining
+ Continued pretraining
+ Fine-tuning
+ LoRA
+ RLHF (to some extent)

You cannot simply "insert" one new fact into parametric memory.

See [non parametric memory](./non-parametric-memory.md)

## Questions

1. What is Pretraining?
2. How is pretraining different from continued pretraining?
3. What is fine-tuning? [fine tuning](/answers/fine-tuning.md)
4. What is LoRA? [LoRA](/answers/lora.md)
5. What is RLHF?
