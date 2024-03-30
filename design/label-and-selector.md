# Label and Selector

Labels allow for objects to be selected, which may not share other characteristics. For example, if a developer were to label their pods using their name, they could affect all of their pods, regardless of the application or deployment the pods were using.

Labels are how operators, also known as watch-loops, track and manage objects. As a result, if you were to hard-code the same label for two objects, they may be managed by different operators and cause issues. For example, one deployment may call for ten pods, while another with the same label calls for five. All the pods would be in a constant state of restarting, as each operator tries to start or stop pods until the status matches the spec.

Consider the possible ways you may want to group your pods and other objects in production. Perhaps you may use **development** and **production** labels to differentiate the state of the application. Perhaps you may want to add labels for the department, team, and primary application developer.



