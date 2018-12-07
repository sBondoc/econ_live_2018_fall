*(For readability purposes, the [.md file](https://github.com/sBondoc/econ_live_2018_fall/blob/master/files/post.md) for this post is available on my GitHub page.)*

# Introduction #

I recently wrote an anecdotal [post](https://sbondoc.blogspot.com/2018/11/doing-laundry.html) on my blog about little things that ultimately add spice to your life in ways that you might not always immediately recognize.

In that entry, I mentioned one of my experiences with the universal college student dilemma: the trade-off between sleeping and doing homework.

Here is an excerpt from that blog post:

>*Should I go lie down in my bed? On one hand, it's cold and lying down is nice. Plus, I'm tired, and I could use a break. On the other hand, I'll probably fall asleep and not get my work done. Well, it's not due until 11 AM, so if I wake up a couple hours before then I'll have time. But will I wake up early? Probably not. But my bed has a blanket, and I like blankets. Then again, it's just physics, so I can probably finish it quickly now and be able to sleep in peace. Then again, it's just physics, so I can probably finish it quickly tomorrow and be able to sleep now. What about lying down with the laptop so I can rest my body but also do the assignment? Nah, I'll probably just fall asleep, so we're back to the first question. I guess sleeping now isn't so bad. But then I won't be able to sleep worry-free. But is there such thing as worry-free? There's always work to be done, and too little time to do it. And aren't all of our fates sealed to the slow decay of our bodies, cell by cell, molecule by molecule, as they succumb to the grips of time until the finality that is the end of our days?*
>
>*Whoa, that escalated quickly. < / stream_of_consciousness >*
>
>*After pausing to think about what I had just thought about and concluding that taking an arbitrary philosophical approach probably wasn't the best way to come to a decision, the idea of using an economic approach popped into my head. I'm taking microeconomics right now, and I couldn't help but think of drawing out a production possibility frontier (PPF), so I did. It was bowed out, since this was a case of increasing opportunity cost. Naturally, this meant that I should've sought a middle ground to balance out the benefits of both options while maximizing efficiency, but again, that would lead back to the "lie down and work" option, which didn't seem likely to happen. I proceeded to write down opportunity costs – like time and energy – of each option and eventually had the whole back side of one of my old physics quizzes covered in random econ stuff. I often think about times like this and of how dumb it is that I do extra work I do to avoid doing other work.*
>
>*Then I remembered I had to do the laundry, so I put my clothes and Tide Pods in the wash and went back upstairs. I finally decided to do my physics homework, since I was already locked in to being awake to finish doing the laundry. While I was doing it, I contemplated whether that was the most efficient decision, constantly worrying that I wouldn't wake up on time and looking up articles on REM sleep and Circadian rhythms to see if I could find a way to determine a time at which to set my alarm guaranteed to wake me up (unfortunately, I found no such method).*
>
>*Once I was about halfway done with my physics homework, I went back down to throw my stuff in the dryer. I went upstairs to continue doing my homework, and in between problem's I'd look at one of the many PPF curves I'd drawn and mentally mark where on the graph I was. For you econ people out there, I'll just say I was inside the bounds of the curve and Vilfredo Pareto would not be proud.*

This is just one of many times that I've had to decide between doing homework and either other homework or some other activity.

# Algorithm #

Being a computer engineering major, I couldn't help but analyze my behavior from a coding perspective. I realized that when I make these decisions, I essentially follow an algorithm that takes in the data of opportunity costs (such as time and energy, mentioned in the excerpt above) and processes it to determine whether or not I end up doing the task and when.

I decided to write down a rough approximation of the process I follow in Python.
	
```python

## Reference 1

def file_to_list(file_name):
  
  file = open(file_name,"r")
  return file.readlines()

## Reference 2

class Course():

  def __init__(self,name = "UCI Course",importance = 0.0,major_required = False)
    
    self.name = name
    self.importance = importance
    self.major_required = major_required
  
  def set_vals(self,file_name):
    
    data_list = file_to_list(file_name)
    
    self.name = data_list[0]
    self.importance = data_list[1]
    self.major_required = data_list[2]    

class Homework():
  
  def __init__(self,name = "Homework Assignment",course = Course(),approx_time = 60.0,point_weight = 10.0,mental_exertion = 10.0,do_now = False):
    
    self.name = name
    self.course = course
    self.approx_time = approx_time
    self.point_weight = point_weight
    self.mental_exertion = mental_exertion
    self.do_now = do_now

## Reference 3

def main():

## Reference 4

  threshold_value_list = file_to_list("threshold.txt")
  threshold_value = threshold_value_list[0]
  to_do_list = []

## Reference 5
  
  course_list = file_to_list("course list.txt")
  courses = []
  homework_list = file_to_list("homework list.txt")
  homework = []
  
  for i in range(len(course_list)):
  
    courses.append(Course(course_list[i]))
    courses[i].set_vals(courses[i].name)
  
  def course(course_name):
  
    for i in range(len(courses)):
      
      if courses[i].name == course_name:
      
        return courses[i]
  
  for i in range(len(homework_list)):
  
    homework.append(Homework(homework_list[i]))
    
    hw_data_list = file_to_list(homework[i].name + ".txt")
    
    homework[i].course = course(hw_data_list[1])
    homework[i].approx_time = hw_data_list[2]
    homework[i].point_weight = hw_data_list[3]

## Reference 5
  
  for i in range(len(homework)):
  
## Reference 6

    if (homework[i].point_weight / (homework[i].approx_time ** 2)) * homework[i].course.importance + homework[i].course.major_required > threshold_value:

## Reference 7

      homework[i].do_now = True
      to_do_list.append(homework[i])

## Reference 8

main()

```

(If you are viewing this on Tumblr, sorry about the lack of color in the code; it appears Tumblr does not support Markdown syntax highlighting in code blocks. It might help if you view the [.md file](https://github.com/sBondoc/econ_live_2018_fall/blob/master/files/post.md) on my GitHub page.)

# Explanation #

Of course, none of that makes sense to someone who hasn't learned how to code, and even someone who knows how to code doesn't necessarily know the syntax and nuances behind developing in Python, so I'll try to explain it in layman's terms.

The section between `## Reference 1` and `## Reference 2` is purely for coding purposes and has nothing to do with economic principles; it defines a utility used later on to use up less lines and make the code easier to read.

The section between `## Reference 2` and `## Reference 3` defines the properties associated with each course you are taking and the homework assignments associated with each course. These properties include what essentially determine opportunity costs of doing the homework, such as the amount of time it might take to do the assignment (`approx_time`), the point impact the assignment has on your grade (`point_weight`), and the effort you'd have to put into the assignment (`mental_exertion`). These values will be used later for determining whether or not to do the assignment at the time this algorithm/thought process is executed.

Up until this point, the code has only been defining tools to use in the main part of the code, which is what actually "does something." Everything between `## Reference 4` and `## Reference 8`refers to this "functional" part of the code.

The way the algorithm works is by adding homework assignments of priority that exceeds a certain arbitrary threshold to a list of assignments that will be done at the time of the decision. The lines between `## Reference 4` and `## Reference 5` define the threshold value (`threshold_value`), which is determined externally from the program, and the section between `## Reference 6` and `## Reference 8` actually create the "to-do list" of homework assignments (`to_do_list`).

The single line between `##Reference 6` and `## Reference 7` is a formula that determines the priority value of the homework assignment. This formula could vary depending on the person, the mood they're in, the kind of day they're having, and other situational things that are difficult to quantify. In this particular formula, I made the priority value of the homework assignment proportional to the relative amount of points it's worth (`homework[i].point_weight`) and the personal importance of the course to the individual (`homework[i].course.importance`). I also made it inversely proportional to the square of the estimated time taken to do the assignment (`homework[i].approx_time ** 2`) because time can be considered an increasing opportunity cost with a bowed-out PPF. Finally, I added a small consideration for whether or not the course is required for the major (`homework[i].course.major_required`).

This algorithm, as previously mentioned, yields a list of assignments to be done, and the actual execution of the algorithm is done in the line after `## Reference 8`.

Altogether, this code, saved as a .py file and run correctly through the Python shell, mimics the decisionmaking process that I undergo when deciding what assignments to do at what time.

# Conclusion #

It goes without saying that procrastination is bad. Ideally, you would never have to run this algorithm for the purpose it is designed for, and you would always have ample time to do your assignments. This code is just for bad planners (like me).

Unfortunately for some, time management isn't exacly a honed skill, leading to situations in which one is backed into a corner faced with a tough decision between undesirable choices. This gets stripped down into an economic decisionmaking problem in its most basic form, built around the fact that people face trade-offs, one of the 10 principles of economics.

I made this code just to illustrate my thought process and how I weigh opportunity costs and trade-offs when it comes to doing my homework. I really hope nobody actually copy/pastes the code into IDLE and uses it to determine how hard they should procrastinate. They'll end up like me, frantically typing an econ assignment up on Tumblr trying to get it in on time for the 5:00 PM due date.
