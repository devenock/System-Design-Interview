# Chapter 3: A FRAMEWORK FOR SYSTEM DESIGN INTERVIEWS

System design interviews are always intimidating. It could be as "vague" as designing a well known product. The questions are ambiguous  and seem unreasonably broad.

The system design interview simulates real-life problem-solving where two co-workers collaborate on an ambiguous problem and come up with a solution that meets their goals.

The final design is always less important as compared to the work you put in the design process. This allows you to demonstrate your design skills, defend your design choices and respond to feedback in a constructive manner.

An effective system design interview gives strong signals about a person's ability to collaborate, to work under pressure and to resolve ambiguity constructively. The ability to ask good questions is also a skill, and many interviewers specifically look for that.

## A 4-step process for effective system design interview
Every system design interview is different. A great system design interview is open-ended and there is no one-size-fits-all solution. However, there are steps and common ground to cover in every system design interview. 

### Step 1 - Understand the problem and establish design scope
In a system design interview, you should not rush to give out quick answers as this is a big red flag. There is always no right answer to the question asked and you should take time to understand the challenge and ask questions to find the right approach of solving it as this is extremely important.

Many engineers like to jump straight to solving a problem however this approach is more likely to lead you to the wrong system. As an engineer, ask the right questions, make proper assumptions and gather all the information needed to build a system.

When you ask questions, an interviewer will either answer you or tell you to make your assumptions. It is always good to write down these assumptions because you will probably need them later. Always ensure that you ask questions to understand the exact requirements.

Here is a list of questions to help you get started:
1. What specific features are we going to build?
2. How many users does the product have?
3. How fast does the company anticipate to scale up? What are the anticipated scales in 3 months, 6 months and a year?
4. What is the company's technology stack? What existing services you might leverage to simplify the design?

### Example
If you are asked to design a news feed system, you might want to ask questions that help you clarify the requirements. This is how the conversation with the interviewer might look:

**Candidate:** Is this a mobile app? web app? or both?

**Interviewer:** Both

**Candidate:** What are the most important features for the product?

**Interviewer:** Ability to make a post and see friends’ news feed.


**Candidate:** Is the news feed sorted in reverse chronological order or a particular order? The particular order means each post is given a different weight. For instance, posts from your close friends are more important than posts from a group.

**Interviewer:** To keep things simple, let us assume the feed is sorted by reverse chronological order.

**Candidate:** How many friends can a user have?


**Interviewer:** 5000

**Candidate:** What is the traffic volume? 

**Interviewer:** 10 million daily active users (DAU)


**Candidate:** Can feed contain images, videos, or just text?

**Interviewer:** It can contain media files, including both images and videos.

Above are some sample questions that you can ask your interviewer. It is important to understand the requirements and clarify ambiguities

