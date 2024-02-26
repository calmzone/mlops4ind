## MLOps course for industry
Feb 25th - Mar 1st, DTU Lyngby

### Day 2, morning
Exercises:
  1. Run and try to grasp what happens in cells. Put your findings/questions into notebook so we can address them: [colab](course/en/day2/transformers.ipynb)
  2.
### Day 2, afternoon

Exercise 
  1. [colab](course/en/day2/HF_wandb.ipynb)
  2. DIY pipeline on your mainframe (laptop):
     1. prepare python environements on your laptop (or use the one of your choice) including torch with support for your metal
     2. clone HF transformers in "editable" install (it updates $PYTHONPATH to include transformers git repository you are about to clone)
        
        ` git clone https://github.com/huggingface/transformers.git`
        
        ` cd transformers`
        
        ` pip install -e .`
        
  4. clone `https://github.com/huggingface/transformers/blob/main/examples/pytorch/language-modeling`
  5. explore and run finetuning `./run_clm.py` in the repository
  6. Task: make it configurable using `hydra` and `wandb`:
     1.) the following replaces trainer.train() from the original script
      ```
          @hydra.main(config_path="./config", config_name="train_gpt2_hf")
          def main(cfg : DictConfig):
          cfg = OmegaConf.to_container(cfg)
          trainer.train(cfg)
          eval_results = trainer.evaluate()
          print(f"Perplexity: {math.exp(eval_results['eval_loss']):.2f}")

          if __name__ == "__main__":
              main()
     ```

     2.) it requires the update of trainer class to work properly with wandb

       * 2a.) import wand and configure wanb in the definition of train() approx. l1308
     
       * 2b.) pass wandb config to train(self,config,...) and to _inner training loop return         inner_training_loop(config=wandb_cfg,...
     
       * 2c.) code logging to wanbd after self.optimizer.step() in the inner training loop, approx. l1678
     
       * 2d.) add additional functions e.g. gradient norms if you like as in the same place in the trainer
     
       * ... there is still one more glitch left - try to figure it out```

Alternative
  4. Follow [this](https://www.philschmid.de/fine-tune-a-non-english-gpt-2-model-with-huggingface) blog showcasing german language and try to teach/finetune GPT2 on danish

Schedule and advanced exercises are available on [hedgehog](https://demo.hedgedoc.org/qCRpSmQ4RoCxLaA3diBJLQ?both) 
