## MLOps course for industry
Feb 26th - Mar 1st, DTU Lyngby

### Day 2, morning
Exercises:
  1. Run and comment on what happens in notebook cells. Put your findings/questions into notebook so we can address them: [colab](course/en/day2/transformers.ipynb)

### Day 2, afternoon
Exercises: 
  1. Setup W&B free account, and play around to get acquainted with W&B logging [colab](course/en/day2/HF_wandb.ipynb)
  2. DIY pipeline on your mainframe (laptop):
     1. prepare python environements on your laptop (or use the one of your choice) including torch with support for your metal
     2. clone HF transformers in "editable" install (it updates $PYTHONPATH to include transformers git repository you are about to clone)
        
        ` git clone https://github.com/huggingface/transformers.git`
        
        ` cd transformers`
        
        ` pip install -e .`
        
  4. clone `https://github.com/huggingface/transformers/blob/main/examples/pytorch/language-modeling`
  5. explore and run finetuning `./run_clm.py` in the repository
  6. If you need read more on Hydra go [here](https://hydra.cc/docs/intro/) and [OmegaConf, .yaml handling](https://omegaconf.readthedocs.io/en/latest/usage.html#access-and-manipulation)
  7. Task: make `./run_clm.py` configurable using `hydra` and `wandb`:
     1.) use Hydra decorator and replace trainer.train() in the following manner (just an example) in `./run_clm.py`
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

       * 2a.) import wand and configure wanb in the definition of train() 
     
       * 2b.) pass wandb config to train(self,config,...) and to _inner_training_loop return inner_training_loop(config=wandb_cfg,...
     
       * 2c.) code logging to wanbd after self.optimizer.step() in the inner training loop
     
       * 2d.) add additional KPIs e.g. gradient norms to W&B dashboard
     
       * ... there is still (and always) one more glitch left - try to figure it out

  Alternative exercises: 
  * Get inspired by [this](https://www.philschmid.de/fine-tune-a-non-english-gpt-2-model-with-huggingface) blog showcasing german language and try to teach/finetune GPT2 on danish. 
  * Even more advanced exercises (ONNX, [Torch ORT] (https://pytorch.org/ort/)) are available [here](https://demo.hedgedoc.org/qCRpSmQ4RoCxLaA3diBJLQ?both) 
