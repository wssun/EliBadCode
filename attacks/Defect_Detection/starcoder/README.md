# Defect Detection
### Fine-tune
```shell
python run.py \
    --output_dir Backdoor/models/Defect_Detection/Devign/StarCoder/poisoned_func_name_substitute_testo_init_True/fft \
    --checkpoint_prefix checkpoint-best-acc \
    --model_type llm \
    --config_name bigcode/starcoderbase-1b \
    --tokenizer_name bigcode/starcoderbase-1b \
    --model_name_or_path bigcode/starcoderbase-1b \
    --do_train \
    --train_data_file Backdoor/dataset/Defect_Detection/Devign/poisoned/train_poisoned_func_name_substitute_testo_init_True.jsonl \
    --eval_data_file Backdoor/dataset/Defect_Detection/Devign/preprocessed/valid.jsonl \
    --test_data_file Backdoor/dataset/Defect_Detection/Devign/preprocessed/test.jsonl \
    --epoch 5 \
    --block_size 400 \
    --train_batch_size 4 \
    --eval_batch_size 4 \
    --learning_rate 2e-5 \
    --max_grad_norm 1.0 \
    --evaluate_during_training \
    --seed 123456  2>&1 | tee train_poisoned_starcoder_fft.log
```

#### Inference
```shell
python run.py \
    --output_dir Backdoor/models/Defect_Detection/Devign/StarCoder/poisoned_func_name_substitute_testo_init_True/fft \
    --checkpoint_prefix checkpoint-best-acc \
    --model_type=llm \
    --config_name bigcode/starcoderbase-1b \
    --tokenizer_name bigcode/starcoderbase-1b \
    --model_name_or_path bigcode/starcoderbase-1b \
    --do_test \
    --train_data_file Backdoor/dataset/Defect_Detection/Devign/preprocessed/train.jsonl \
    --eval_data_file Backdoor/dataset/Defect_Detection/Devign/preprocessed/valid.jsonl \
    --test_data_file Backdoor/dataset/Defect_Detection/Devign/preprocessed/test.jsonl \
    --epoch 5 \
    --block_size 400 \
    --train_batch_size 16 \
    --eval_batch_size 16 \
    --learning_rate 2e-5 \
    --max_grad_norm 1.0 \
    --evaluate_during_training \
    --seed 123456 2>&1 | tee test_clean_starcoder.log

cd ..
python evaluator.py
```
