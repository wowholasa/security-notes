# Mandatory Hand-in 2

## Description

Alice, Bob and Charlie are participating in a medical experiment in their local Hospital where they need to provide data for training a Machine Learning (ML) model, which will later be used to diagnose patients. In this setting, the Hospital runs a central server that collects data from all patients. The Hospital is trusted to honestly execute a data collection protocol pre-agreed among all patients taking part in the experiment. However, the Hospital is aware of security issues and does not want to store this data in its systems. Moreover, do not trust each other to see their data, but do trust each other to follow the protocol established by the Hospital. As usual, the patients and the Hospital communicate over the Internet.

The restrictions in the scenario above leave the Hospital and patients in a tight spot, since standard ML algorithms require access to plaintext data in order to train a model. Luckily, the researchers in the hospital are collaborating with a team of security experts who suggested using a Federated Learning algorithm that supports Secure Aggregation, which allows the algorithm to train a model while seeing only an aggregate value computed from all patients' data. In particular, this algorithm works on aggregated values obtained by summing all individual patient's values. Using this technique, neither the patients nor the Hospital get access to patient's individual plaintext data, but only to aggregated values.

1) Reflect on this scenario in the context of the GDPR: What are the potential issues in having the hospital store plaintext private data provided by patients even if they have consented to participate on the experiment and have their data processed? Would these issues be solved by removing the patients' names from their data before storing it?  What are the remaining risks in using Federated Learning with Secure Aggregation as suggested?

2) Design and implement a solution that allows for the 3 patients and the Hospital in the scenario above to compute an aggregate value of the patients' private input values in such a way that the Hospital only learns this aggregate value and no patient learns anything besides their own private inputs. Your protocol must also ensure confidentiality and integrity of the data against external attackers. Consider that all individual values held by patients are integers in a range [0,...,R] and that the aggregated value is the sum of all individual values, which is also assumed to be in the same range. You must describe an adversarial model (or threat model) capturing the attacks by an adversary who behaves according to the scenario described above, explain how your solution works and why it guarantees security against such an adversary.

Hint: Secure Aggregation for Federated Learning is a real-world practical technique.

Deliverables:

- A written report reflecting on the questions in "1", describing the adversarial model you are working on, describing the building blocks of your proposed solution, how they are combined in your final solution and why they guarantee security against the adversary you describe.
- An implementation of your solution in a programming language of your choosing, along with clear instructions on how to compile and run it (potentially added to the report or to a separate Readme file).

Submission Instructions:

- This is an INDIVIDUAL hand-in.
- Submit only the PDF file with your report and the file containing your code. Do not submit whole folders containing metadata, auxiliary IDE files or anything else than the code and report.
- Please name your submission clearly using your Name/Student ID, e.g. Jane Doe - 36476832.zip, Jane Doe - 36476832 - Report.PDF, Jane Doe - 36476832 - code.c, Jone Doe - 36476832 - Readme.txt. This makes grading faster, so that you get feedback on your hand-in faster.

## Notes:

Data: Health data

Data needs to be fixed when processed

Patients should not be able to see other patients’s data

Secure aggregation

Just an addition of the patients data point

Design a solution that allows the hospital to only know the sum of patient data points and the patients learn nothing besides their own data. 

What adversary should be considered? Why does the solution provide protection against the adversary

What GDPR risks remain in the solution? 

This is preparation for the exam. Similar things will be on the exam, just without the coding part.

Adversary: 

Passive adversary since the patients trust each other to follow protocol, but not with their data.

Dolev-Yao, since we are transferring data over a network.

Why is the data GDPR sensivitive?: Because it can be used to identify an individual

How can we design a solution that protects against our adversaries?: Certificates and TLS

DON’T TRY TO DESIGN YOUR OWN CRYPTOGRAPHIC PROTOCOL

Explain why TLS solves the problem.

TLS gives very specific guarantees.

You need an infrastructure (certificate etc) to use TLS.

A secret sharing scheme that splits a secret into a random number of shares so no single share can find the secret (lecture 6?)

Using threshold secret sharing that is a scheme that helps reconstruct a secret sharing scheme. Not a requirement here, but very good to have in the real world.

How do we use secret sharing in this scenario?: 

- Make sure that you do not reveal too much.
- Run a protocol.
- The output we want is the addition of all the shares
- Only patients would get a share of each patients input
- Each patient to get shares of their own input and they distribute their shares to other patients.

Adversaries do not break from protocol as they are passive. All they can see is their local input. We do not want the adversary to see private inputs of patients.

Argue why your solution is secure against a private adversary that corrupts that many parties and why an adversary can corrupt up to X parties (Where X is the limit that you allow the adversary to corrupt)

Set your secret sharing threshold that given a number of corruptions you will not be revealing more information about the honest parties input that they would not already be learning.

We want to protect the honest parties <3 because they are so precious. Being honest is good tihi

Explain what secret sharing scheme you are using, how that scheme works, and… I didn’t hear

You can put a restriction on your dolev-yao adversary that it will not drop messages, since Bernardo doesn’t want us to focus on availability.

Use a TLS library. NEVER IMPLEMENT TLS