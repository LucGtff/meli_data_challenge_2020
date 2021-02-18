# meli_data_challenge_2020

Here are the main files used for my participation to the [Meli data challenge 2020](https://ml-challenge.mercadolibre.com/). 

This is my first participation to a data challenge.  Here, the goal was to "Build a Machine Learning model to predict next purchase based on the user’s navigation history." It was a nice experience in a field I had no experience (e commerce) and I enjoyed it. [I ranked 31](https://ml-challenge.mercadolibre.com/final_results)  out of more than 120, this motivated me to participate to other challenges. 

# Problem analysis and strategie put in place

(WORKING ON PROGRESS)

•	I divide my solution in two steps. First looking for the domain, then looking for the best combination of items. 

•	To predict the domain_id:
o	First, I focused on the “view” event_type only, looking to predict the domain when being present in history. After some analysis, I ended up thinking that the most valuable information was the rank based, ie affecting at each domain_id in history some ranks:
	its rank in term of date, the latest viewed being the first, the second latest 2, etc…its rank in term of how many items have been viewed in it, its rank in term of the max number of views of one particular item also 
	I had the feeling that the category_id was useless 
	I try to see if it was worth to use the info in a more précised than their rank only, but I could not conclude anything 
	Here, I did try easy solution, proposing the latest domain, or the one with max number, etc… eventually looking for combination, given that I could propose 10 item_id, hence from 2, or 3 different domains. For each of these strategies, I started computing the NCDG, taking the list of their existing items in the history. I did it with few simulations, since the convergence seemed pretty quick and I had some values at 0.25 more or less, 
o	Then I thought that I could use a ML algo - a logistic regression - to keep thing as simple as possible, based on all this rank information. The NCDG seemed to improve a bit, but very slightly. I even wonder if the improvement was significant.
o	I then tried to use a xgboost, trying to use some more advanced ML algo, tried to move some hyper parameters, but I did not see lots of move in the result, hence I thought that the way I design my solution, based on these ranks, could not be improved at all .
o	Then, I thought that I could use the info from the “search”, using rank as well. I tried to rank the domain_id viewed in history, with their connection with the search made. Something like “what is the domain_id viewed in history, which seemed more similar with the searchs, the last one, the one which occurred more frequently, etc… Unfortunately, it gave no result. (*)

•	Then, to predict the best combination of items in a domain_id
o	I started with something easy, like the latest items_id visited, the ones visited much time, etc… and completing the list with random items_id from the domain_id 
o	Then I thought that to complete the list, I could propose better item_id, than choosing them randomly. I tried the ones the most bought within the domain_id (following the idea from the meli guy in the video). I had the feeling that it did improve my result, but in a very slightly way 
o	I tried also the items which had the more similar title (with counting manually the number of words, wondered if some nlp things could be better), slight or even no improve here

•	When no “view”, or very few “views” with respect to the “search”, looked for the domain_id with words more similar to the “search”, in the same idea as in (*). But it looked that this method was not very useful compared to taking profit of the analysis of “view” when existing. 

	I suppose if it was possible to predict the domain_id by mixing up in a more consistent way the “view” and the “search” 
	I suppose I did not extract the best information of the dataset with my ranks 
	Using more advanced ML algo should be probably useful, but in the way I have designed my strategy, I don’t think so. 
	Maybe some more detailed analyses, domain_id by domain_id could be relevant. I did not enter into this. 
	In the end, I am happy with my NCDG 0.25, but I guess this value is mainly based on something very simple, proposing the items more frequent, and seen the latest in the history, and complete the list with items of their domains. All the things more advanced have probably an impact, nothing very significant I believe. 
