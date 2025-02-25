<h1 align="center"> <a href="">Reasoning Attack: Inducing LLM to Never-End Thinking</a></h1>
<h5 align="center"> If you like our project, please give us a star ⭐ on GitHub for latest update.  </h5>


# 📖Overview
Reasoning LLMs, like DeepSeek-R1, trained via large-scale reinforcement learning(RL) have demonstrated remarkable reasoning capabilities. 
However, they will be trapped in over-reasoning even endless thinking when processing some special queries. 
With such never-end thinking queries, hackers can crack down a model server in a cheaper DDoS way for that a single query would occupy the resources until reaching maximal tokens constraint. 
This catastrophe bug, never-end thinking query, will undermine the open-source development eco-system relies on reasoning LLMs. In this report, we release a reasoning attack pipeline cracking LLM Reasoning models, finding those over-reasoning queries. 
Worse still, those queries can transfer across the same series of distilled models. 
We do hope the community could find solution to the bug soon preventing from being exposure to potential threats. 

![pipeline](https://github.com/user-attachments/assets/82b8bb9d-b21b-433e-b7b2-79f3d8576826)

# 💡Highlights

* the reasoning model will not generate the end thinking token `</think>`
* the same over-reasoning query can transfer across the same series of distilled models.
* the reasoning model would repeat some sequences until running out of tokens.
* the open-source development eco-system relying on reasoning LLMs is under danger of a new DDoS attack


# 🤗Main results

## Attack Demo
we exhibit some typical reasoning attack demo manipulating the DeepSeek-R1 series of models generating extremely long thinking CoT process. 
The attack prompt "树中两条路径之间的距离" can manipulate the whole DeepSeek-R1 series of models generate endless CoT until running out of max token length constraint.

https://github.com/user-attachments/assets/a67ad7c7-9c39-4cfb-9444-58e494ff48ae

https://github.com/user-attachments/assets/f8a4a8cf-6208-40cb-a480-cf01b9b5a203

https://github.com/user-attachments/assets/33844deb-8baf-45cc-9676-40a8cc56b670

https://github.com/user-attachments/assets/60a29932-4c20-497e-8470-c03df9b4130b


## Repetitive Sequence
![](assets/repetitive-demo.jpg)

## DDoS
The over-reasoning attack queries can persistently occupy relatively massive computing resources, however, the hackers only pay for it with tiny network resources. 
We run a toy experiment on comparing over-reasoning queries and normal queries computing resources occupation. 
We deploy DeepSeek-R1-Distill-Qwen-1.5B on a single Nvidia 4090 GPU, running over-reasoning query and normal query recording their GPU occupation as following.
As shown in figure, with only a few over-reasoning request will take the whole GPU resource, it would be a nightmare that hacker take the property as a DDoS tactic to attack servers.

![](assets/GPU-Occupation.jpg)

# 💬Discussion

## Causation
We suppose the exploration in RL training leads to the over-reasoning due to promoting exploration strategy during sparse reward training. 
For most normal common users' queries won't last long and repetitive CoT, so it's would be a temporary strategy to limit the maximum length of CoT, relieving malicious DDoS. 
For the long term, it's wiser to address the issue of unstably extending CoT length and complexity in RL training

## Future Work
We have discussed the basic character of never-end thinking query, but we still not demystify the fundamental causation of the never-end thinking query. 
We will continue working on its causation through its RL based training process and exploring potential defense methods like stable CoT extension.

# Contact
* Jiayu Yao: jiayu_yao@pku.edu.cn
* Kunpeng Ning: ningkp@stu.pkeu.edu.cn

