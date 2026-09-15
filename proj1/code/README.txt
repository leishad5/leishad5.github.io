HOW TO RUN THE CODE:
When you open main.ipynb, just run all the cells. The last cell will output the offset measurements and the alignment times per image. 
It will also save all of the aligned images into 'web/media/out'.

HOW THE CODE WORKS:
To write the code for this project, I split up the tasks into a few helper functions, then adjusted the skeleton code provided to process the image.

I made an image pyramid function that uses the single scale alignment automatically on images with a smallest pixel dimension less than 400, since the JPEGs had a width of 390 and height of <350.
For larger images, the image pyramid function resizes both images to be 1/4 of the area, then runs the image pyramid on the subproblem. If the resized image is still larger than the base case, the image continues downsizing by 1/4.
Once the image is at least as small as the base case, the single scale alignment is performed at each level, and the offsets at each level are saved and propogated up the recursive pathway to save time 
(i.e. the start point for the fine-tuned search one level up is decided by the previous coarse alignment). 
The align function takes in a cropped image and uses the roll function to shift the overlay image (R or G) by whatever the optimal offsets are. 
The optimal offsets are determined by the similarity function, which can be calculated via L2 or NCC, depending on the user's entry. 
The file name, search window, crop percentage, and similarity metric are decided by the user. 