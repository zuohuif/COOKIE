# COOKIE: A Dataset for Conversational Recommendation over KnowledgeGraph in E-commerce

[Download here](https://drive.google.com/drive/folders/1gOIsuy3RSqi3UbTnfYyzgVS7msQVRKU5?usp=sharing)

### Dialog-related Files
| File                            | Description | Format |
|---------------------------------|-------------|--------|
| dial_utter_resp_train.npz       | Training utterances & responses. | An npz object with 3 variables. <br> - var1: `utterance` is a numpy array of size `#user_item_pairs x #utters x utter_len`. <br> - var2: `response` is a numpy array of size `(#user_item_pairs x 2) x utter_len`. <br> - var3: `label` is a numpy array of size `(#user_item_pairs x 2)`. Label `1` indicates correct response while `0` is wrong response. |
| dial_utter_resp_val.npz         | Validation utterances & responses. | An npz object with 3 variables. <br> - var1: `utterance` is a numpy array of size `#user_item_pairs x #utters x utter_len`. <br> - var2: `response` is a numpy array of size `(#user_item_pairs x 10) x utter_len`. <br> - var3: `label` is a numpy array of size `(#user_item_pairs x 10)`. Label `1` indicates correct response while `0` is wrong response. |
| dial_utter_resp_test.npz        | Test utterances & responses. | An npz object with 3 variables. <br> - var1: `utterance` is a numpy array of size `#user_item_pairs x #utters x utter_len`. <br> - var2: `response` is a numpy array of size `(#user_item_pairs x 10) x utter_len`. <br> - var3: `label` is a numpy array of size `(#user_item_pairs x 10)`. Label `1` indicates correct response while `0` is wrong response.  |
| dial_word_embed.npz             | Word embeddings for dialogs. | An npz object with 1 variables. <br> - var1: `word_emb` is a numpy array of size `#(num of words + 1) x #200`, the last word index is padding index. |
| dial_gt_context_train.npz | Groundtruth entities and KG context triples for training utterances. | An npz object with 4 variables. <br> - var1: `utter_gt` is a numpy array of size `#user_item_pairs x #utters x 1`. <br> - var2: `utter_context` is a numpy array of size `#user_item_pairs x #utters x (#triples x 3)`. <br> - var3: `resp_gt` is a numpy array of size `(#user_item_pairs x 2)`. <br> - var4: `resp_context` is a numpy array of size `(#user_item_pairs x 2) x (#triples x 3)`. |
| dial_gt_context_val.npz   | Groundtruth entities and KG context triples for validation utterances. | An npz object with 4 variables. <br> - var1: `utter_gt` is a numpy array of size `#user_item_pairs x #utters x 1`. <br> - var2: `utter_context` is a numpy array of size `#user_item_pairs x #utters x (#triples x 3)`. <br> - var3: `resp_gt` is a numpy array of size `(#user_item_pairs x 10)`. <br> - var4: `resp_context` is a numpy array of size `(#user_item_pairs x 10) x (#triples x 3)`. |
| dial_gt_context_test.npz  | Groundtruth entities and KG context triples for test utterances. | An npz object with 4 variables. <br> - var1: `utter_gt` is a numpy array of size `#user_item_pairs x #utters x 1`. <br> - var2: `utter_context` is a numpy array of size `#user_item_pairs x #utters x (#triples x 3)`. <br> - var3: `resp_gt` is a numpy array of size `(#user_item_pairs x 10)`. <br> - var4: `resp_context` is a numpy array of size `(#user_item_pairs x 10) x (#triples x 3)`. |

*Notes:*
- `#utters`=10, `utter_len`=50, `#triples`=8.
- `#user_item_pairs` depends on train/validation/test.

### Recommendation-related Files
| File                      | Description | Format |
|---------------------------|-------------|--------|
| rec_train.txt             | Training user-item pairs used as purchase history. | Each row is a user-item pair in the form of `[user_id]\t[item_id]`. The i-th row corresponds to the i-th dialog in the "dial_utter_resp_train.npz" file. |
| rec_val_candidate100.npz  | Validation user-item pairs including 101 candidates. | An npz object with 1 variable. <br> - var1: `candidates` is a numpy array of size `#user_item_pairs x 102`, where the first column is user id, second column is groundtruth item id and the rest 100 columns are negative item ids. |
| rec_test_candidate100.npz | Test user-item pairs including 101 candidates. | An npz object with 1 variable. <br> - var1: `candidates` is a numpy array of size `#user_item_pairs x 102`, where the first column is user id, second column is groundtruth item id and the rest 100 columns are negative item ids. |

*Notes:* 
- `[user_id]` and `[item_id]` refer to the entity id of users and items in KG.

### KG-related Files
| File                  | Description | Format |
|-----------------------|-------------|--------|
| kg_user_entities.txt  | User entities. | Each row is `user::[username]\t[entity_id]`. |
| kg_item_entities.txt  | Item entities. | Each row is `product::[item_name]\t[entity_id]`. |
| kg_other_entities.txt | Other entities. | Each row is `[entity_type]::[entity_name]\t[entity_id]`. |
| kg_relations.txt      | Relations (no inverse relation included). | Each row is `[relation_name]\t[relation_id]`. |
| kg_train_triples.txt  | Training triples regarding user-item interactions. | Each row is `[head_entity_id]\t[tail_entity_id]\t[relation_id]`, where the `[relation_id]` is always `0` meaning the user-item interaction. |
| kg_other_triples.txt  | Other triples excluding user-item interactions. | Each row is `[head_entity_id]\t[tail_entity_id]\t[relation_id]`. |

*Note: user entity ids, item entity ids and other entity ids are consecutive. E.g., suppose there are 100 users, 200 items and 500 other entities. The user ids range in [0, 99], item ids range in [100, 299] and other entity ids range in [300, 799].* 

## Baselines

### DMN[1]
Follow the process [here](https://github.com/yangliuy/NeuralResponseRanking).
### OpendialKG[2]
Comming Soon!
### MSN[3]
Comming Soon!
## Reference
[1] Liu Yang, Minghui Qiu, Chen Qu, Jiafeng Guo, Yongfeng Zhang, W. Bruce Croft, Jun Huang, Haiqing Chen. "Response Ranking with Deep Matching Networks and External Knowledge in Information-seeking Conversation Systems", In Proceedings of SIGIR. 2018.

[2] Seungwhan Moon, Pararth Shah, Anuj Kumar, Rajen Subba. "OpenDialKG: Explainable Conversational Reasoning with Attention-based Walks over Knowledge Graphs", In Proceeding of ACL. 2019.

[3] Qibin Chen, Junyang Lin, Yichang Zhang, Ming Ding, Yukuo Cen, Hongxia Yang, Jie Tang. "Towards Knowledge-Based Recommender Dialog System", In Proceeding of EMNLP. 2019.


