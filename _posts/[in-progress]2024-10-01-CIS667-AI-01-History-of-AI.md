# The History of Artificial Intelligence

A quick way to summarize the milestones in AI history is to list the Turing Award winners: 
1. Marvin Minsky (1969) and John McCarthy (1971) for defining the foundations of the field based on representation and reasoning
2. Ed Feigenbaum and Raj Reddy (1994) for developing expert systems that encode human knowledge to solve real-world problems
3. Judea Pearl (2011) for developing probabilistic reasoning techniques that deal with uncertainty in a principled manner
4. Yoshua Bengio, Geoffrey Hinton, and Yann LeCun (2019) for making “deep learning” (multilayer neural networks) a critical part of modern computing.

The rest of this section goes into more detail on each phase of AI history.

## 1. **The inception of artificial intelligence (1943–1956)**

The first work recognized as AI began with Warren McCulloch and Walter Pitts in 1943. Inspired by mathematical modeling from Pitts’ advisor, Nicolas Rashevsky, they combined three key elements: 
- knowledge of the basic physiology and function of neurons,
- formal analysis of propositional logic by Russell and Whitehead,
- and Turing’s theory of computation. 

They developed a model of **artificial neurons**, each functioning as “on” or “off,” where neurons activate in response to sufficient stimulation from neighboring neurons. They demonstrated that any computable function could be carried out by a network of connected neurons and that logical operations such as AND, OR, and NOT could be executed by simple network structures. 

McCulloch and Pitts also proposed that these networks could learn. In 1949, **Donald Hebb** introduced a simple rule for modifying connections between neurons, known today as **Hebbian learning**, a foundational model that remains relevant.

In 1950, Harvard undergraduates **Marvin Minsky** and **Dean Edmonds** built the first neural network computer, the **SNARC**, using 3,000 vacuum tubes and surplus parts from a B-24 bomber to simulate a network of 40 neurons. Later, Minsky’s Ph.D. work on neural networks at Princeton received skepticism, but **von Neumann** famously remarked, “If it isn’t now, it will be someday,” foreseeing its importance.

Other early AI efforts included checkers-playing programs developed independently by **Christopher Strachey** at Manchester University and **Arthur Samuel** at IBM in 1952. However, **Alan Turing's** vision was the most influential. His 1950 paper, *Computing Machinery and Intelligence,* introduced key AI concepts like the **Turing Test**, **machine learning**, **genetic algorithms**, and **reinforcement learning**. Turing believed creating human-level AI would be easier through learning algorithms rather than programming intelligence manually, although he warned this might not be the best outcome for humanity.

In 1955, **John McCarthy** from Dartmouth College brought together prominent researchers, including Minsky, **Claude Shannon**, and **Nathaniel Rochester**, to organize a summer workshop at Dartmouth in 1956. The aim was to explore the idea that every aspect of learning and intelligence could be precisely described and simulated by machines. Participants included **Allen Newell** and **Herbert Simon**, who presented the **Logic Theorist (LT)**, a mathematical theorem-proving system capable of solving problems non-numerically. LT successfully proved most of the theorems in Russell and Whitehead's *Principia Mathematica*, even finding a shorter proof for one theorem. Despite the significance of their work, the **Journal of Symbolic Logic** rejected a paper co-authored by Newell, Simon, and the Logic Theorist.

Although the Dartmouth workshop didn’t lead to immediate breakthroughs, it laid the foundation for AI as a formal field of study.

*Reference Papers:*
1. [Warren McCulloch and Walter Pitts' 1943 paper on artificial neurons](https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf)
   - https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf
2. [Donald Hebb's 1949 work introducing Hebbian learning](https://doi.org/10.7551/mitpress/4943.003.0006)
   - https://doi.org/10.7551/mitpress/4943.003.0006
3. [Alan Turing's 1950 paper "Computing Machinery and Intelligence"](https://courses.cs.umbc.edu/471/papers/turing.pdf)
   - https://courses.cs.umbc.edu/471/papers/turing.pdf
4. [Arthur Samuel's 1952 work on checkers-playing programs](https://link.springer.com/content/pdf/10.1007/978-0-387-76576-1_7.pdf)
   - https://link.springer.com/content/pdf/10.1007/978-0-387-76576-1_7.pdf
5. [Christopher Strachey's 1952 work on checkers-playing programs](https://dl.acm.org/doi/abs/10.1145/800259.808992)
   - https://dl.acm.org/doi/abs/10.1145/800259.808992
6. [The paper on the Logic Theorist by Allen Newell and Herbert Simon, presented at the 1956 Dartmouth Conference](https://bitsavers.org/pdf/rand/ipl/P-850_Current_Developments_In_Complex_Information_Processing_May56.pdf)
   - https://bitsavers.org/pdf/rand/ipl/P-850_Current_Developments_In_Complex_Information_Processing_May56.pdf
7. Russell and Whitehead's "Principia Mathematica," which is not a research paper but a seminal work in mathematical logic that the Logic Theorist proved theorems from.

## 2. **Early enthusiasm, great expectations (1952–1969)**

## 3. **A Dose of Reality (1966–1973)**

From the outset, AI researchers made bold predictions about their impending successes. One frequently cited statement by **Herbert Simon** in 1957 claims:  
*"It is not my aim to surprise or shock you—but the simplest way I can summarize is to say that there are now in the world machines that think, that learn and that create. Moreover, their ability to do these things is going to increase rapidly until—in a visible future—the range of problems they can handle will be coextensive with the range to which the human mind has been applied."*

Simon went further, predicting that within 10 years, a computer would become a chess champion and that machines would prove significant mathematical theorems. While these predictions did eventually come true, it took around 40 years, not 10. Simon’s overconfidence stemmed from the promising early performance of AI systems on simple tasks, but these systems often failed when confronted with more complex problems.

There were two primary reasons for these failures:
  1. **Informed Introspection**: Early AI systems were often designed based on intuitive guesses about how humans perform tasks, rather than careful task analysis. This approach did not account for what it truly meant to solve a problem or the algorithmic requirements necessary to consistently achieve solutions.
  2. **Intractability**: AI researchers underestimated the **computational complexity** of many problems. Early systems relied on brute-force approaches, trying different combinations of steps until a solution was found. These methods worked in simple "microworlds" with few objects and limited actions, but they collapsed when scaled to more complex scenarios. For example, resolution theorem proving quickly became impractical as researchers attempted to prove theorems involving more than a few dozen facts.

Another significant factor contributing to AI's struggles was the illusion of **unlimited computational power**. This was not limited to problem-solving systems but also extended to early experiments in **machine evolution** (now known as genetic programming). Researchers such as **Friedberg** (1958) believed that by making small mutations to machine code and selecting useful mutations, they could evolve programs that performed well on specific tasks. Despite vast amounts of CPU time, these experiments made almost no progress.

The failure to address **combinatorial explosion**—the exponential increase in possible solutions with problem size—was one of the key criticisms in the **Lighthill Report** (1973). This report led the British government to cut AI research funding at most universities, except for two. Although political and personal factors also played a role, the fundamental technical difficulties were undeniable.

A third issue was the **limitations of early neural networks**. In their 1969 book *Perceptrons*, **Minsky and Papert** demonstrated that simple neural networks (perceptrons) could only learn tasks they were capable of representing, and their representational capacity was severely limited. For instance, a perceptron with two inputs could not be trained to recognize when the inputs were different. Although their analysis didn’t apply to more complex, multilayer networks, this work contributed to a dramatic reduction in funding for neural network research.

Ironically, the **back-propagation learning algorithms**, which would revive neural networks in the late 1980s and 2010s, had already been developed in the early 1960s by **Kelley** (1960) and **Bryson** (1962) in different contexts, but they remained relatively unknown until much later.


## 4. **Expert systems (1969–1986)**


## 5. **The Return of Neural Networks (1986–Present)**

In the mid-1980s, at least four separate research groups independently reinvented the **back-propagation learning algorithm**, which had originally been developed in the early 1960s. This algorithm was quickly applied to a variety of learning problems in both computer science and psychology. The publication of these results in the influential work *Parallel Distributed Processing* by **Rumelhart and McClelland** (1986) sparked widespread excitement in the field.

These models, known as **connectionist models**, were seen by some as direct competitors to the **symbolic models** championed by researchers like **Newell and Simon** and the **logicist approach** of **McCarthy** and others. It may seem obvious that humans manipulate symbols at some cognitive level; in fact, anthropologist **Terrence Deacon** suggested in his book *The Symbolic Species* (1997) that symbol manipulation is a defining characteristic of humans. However, **Geoff Hinton**, a major figure in the resurgence of neural networks in both the 1980s and 2010s, famously referred to symbols as the "luminiferous aether of AI," alluding to the now-disproven 19th-century belief in a medium through which electromagnetic waves propagate. 

Connectionist models offer a different perspective from symbolic AI. While early AI researchers hoped to define concepts through rigid, logically necessary and sufficient conditions, these efforts often fell short when confronted with the complexities of the real world. **Connectionist models** may form internal representations of concepts in a more flexible, imprecise way, potentially making them better suited for handling real-world variability. 

A key strength of these models is their ability to **learn from examples**. By comparing their predicted outputs to the true values, neural networks can adjust their internal parameters through **backpropagation** to minimize errors. This process allows them to improve performance on future tasks, making them highly adaptable to new learning problems. This capability, coupled with their resurgence in the 2010s, has solidified neural networks as a fundamental approach in AI research and application.

## 6. **Probabilistic Reasoning and Machine Learning (1987–Present)**

The limitations of early **expert systems** led to a shift in AI towards a more scientific approach, focusing on **probability** rather than Boolean logic, **machine learning** rather than hand-coded rules, and emphasizing **experimental results** over philosophical arguments. Instead of proposing entirely new theories, AI researchers began building on existing work, ensuring claims were backed by rigorous theorems or solid experimental methods (Cohen, 1995), and demonstrating applicability to real-world problems.

During this period, AI embraced benchmark problem sets such as the UC Irvine repository for machine learning datasets and the **International Planning Competition**. AI also began to integrate insights from related fields like **control theory** and **statistics**, moving away from isolationism. As David McAllester (1998) noted, AI no longer stood apart from other disciplines but rather recognized the value of linking machine learning to information theory, uncertain reasoning to stochastic modeling, and automated reasoning to formal methods and optimization.

An illustrative example is **speech recognition**. In the 1970s, many different architectures were tested, but they were often ad hoc and fragile, limited to a few select examples. By the 1980s, **Hidden Markov Models (HMMs)** emerged as the dominant approach due to their mathematical rigor and ability to be trained on large corpora of real speech data, steadily improving performance in blind tests. This mathematical foundation, combined with data-driven training, allowed speech recognition and handwritten character recognition to transition into industrial and consumer applications.

Another major milestone in 1988 was **Judea Pearl's** work on **Probabilistic Reasoning in Intelligent Systems**, which introduced **Bayesian networks**—a formalism for representing uncertain knowledge efficiently and offering practical algorithms for probabilistic reasoning. This work led to the broader acceptance of **probability theory** and **decision theory** within AI. Since then, probabilistic formalisms have become more expressive, and learning Bayesian networks from data has expanded in applications.

In the same year, **Rich Sutton** connected **reinforcement learning**—previously used in Arthur Samuel’s checker-playing program in the 1950s—with the theory of **Markov Decision Processes (MDPs)** from operations research. This link provided a solid theoretical foundation for reinforcement learning, which was then applied to areas like **robotics** and **process control**.

This period saw the reintegration of subfields like **computer vision**, **robotics**, **speech recognition**, **multiagent systems**, and **natural language processing**, which had become somewhat separated from core AI. This reunification yielded both practical benefits, such as the deployment of robots in industry, and deeper theoretical understanding of AI's core problems. AI's newfound appreciation for **data**, **statistical modeling**, **optimization**, and **machine learning** marked a significant turning point in its evolution.

## 7. **Big Data (2001–Present)**

The rise of **big data** has been driven by remarkable advances in computing power and the expansion of the World Wide Web, which enabled the creation and access to extremely large data sets. These data sets include trillions of words of text, billions of images, and vast amounts of speech, video, genomic data, vehicle tracking data, clickstream data, social network data, and more.

This explosion of data has led to the development of specialized **learning algorithms** designed to harness and process massive datasets. A significant portion of these data sets is often unlabeled, as demonstrated in Yarowsky's (1995) influential work on **word-sense disambiguation**. For example, the word “plant” may appear in a dataset without labels to clarify whether it refers to flora or a factory. Despite this, with large enough datasets, suitable learning algorithms can achieve impressive accuracy—over 96% in distinguishing the intended meaning of ambiguous words in sentences.

Research by Banko and Brill (2001) showed that increasing the size of a dataset by two or three orders of magnitude often leads to greater performance improvements than refining the algorithm itself. This trend has also been observed in **computer vision** tasks, such as filling in missing sections of images. Hays and Efros (2007) developed a method that blends pixels from similar images to fill gaps, but the quality of their technique improved dramatically when moving from thousands to millions of images. This jump in performance highlighted the critical role of big data, and the availability of tens of millions of images in the **ImageNet** database (Deng et al., 2009) sparked a revolution in computer vision.

The availability of big data, combined with the shift toward **machine learning**, helped restore the commercial appeal of AI (Havenstein, 2005; Halevy et al., 2009). A notable example of big data's impact was the 2011 victory of **IBM's Watson** system over human champions in the quiz game *Jeopardy!*, which significantly influenced public perception of AI's capabilities.


## 8. **Deep learning (2011–present)**
Deep learning refers to machine learning models that utilize multiple layers of simple, adjustable computing elements. Although experiments with such networks date back to the 1970s, and convolutional neural networks (CNNs) achieved some success in tasks like handwritten digit recognition in the 1990s (LeCun et al., 1995), it wasn't until 2011 that deep learning truly took off, beginning with speech recognition and later visual object recognition.

A major breakthrough came in the 2012 ImageNet competition, which involved classifying images into one of a thousand categories (e.g., armadillo, bookshelf, corkscrew). A deep learning system developed by Geoffrey Hinton’s team at the University of Toronto (Krizhevsky et al., 2013) demonstrated a dramatic improvement over previous systems, which largely relied on handcrafted features. Since then, deep learning systems have surpassed human performance in several vision-related tasks (though not all), and similar gains have been achieved in speech recognition, machine translation, medical diagnosis, and game playing. Notably, AlphaGo, powered by deep networks representing its evaluation function, defeated leading human Go players (Silver et al., 2016, 2017, 2018).

These impressive successes have sparked a resurgence of interest in AI from various sectors, including students, businesses, investors, governments, and the media. Nearly every week brings news of new AI applications that approach or exceed human capabilities, leading to speculation about either rapid future advances or the possibility of another "AI winter."

Deep learning heavily relies on powerful hardware. While a standard CPU can perform around $10^9$ to $10^10$ operations per second, deep learning algorithms, especially when run on specialized hardware like GPUs, TPUs, or FPGAs, can execute between $10^14$ and $10^17$ operations per second. These operations, primarily in the form of highly parallelized matrix and vector calculations, are crucial for deep learning’s performance. Additionally, the success of deep learning depends on the availability of vast amounts of training data and a few critical algorithmic techniques.






