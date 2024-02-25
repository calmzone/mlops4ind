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
        
  4. clone 

Alternative
  4. Follow [this](https://www.philschmid.de/fine-tune-a-non-english-gpt-2-model-with-huggingface) blog showcasing german language and try to teach/finetune GPT2 on danish

Schedule and advanced exercises are available on [hedgehog](https://demo.hedgedoc.org/qCRpSmQ4RoCxLaA3diBJLQ?both) 
