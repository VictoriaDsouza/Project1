version: 2.1


jobs:
  one:
    docker:
        - image: cimg/ruby:2.6.8
    steps:
      - checkout
      - run: echo "A first hello"
      - run: mkdir -p my_workspace
      - run: echo "Trying out workspaces" > my_workspace/echo_output
      - persist_to_workspace:
          root: my_workspace
          paths:- echo-output
  two:
    docker:
        - image: cimg/ruby:2.6.8
    steps:
      - checkout
      - run: echo "A first hello 3"
      - attach_workspace:
          at:my_workspace
      - run: |
            if [[$(cat my_workspace/echo_output) == "Trying out"]]; then
            echo "It worked!";
      
workflows:
    one_and_two:
      jobs:
        - one
        - two : requries: -one




version: 2
jobs:
  one:
    docker:
        - image: cimg/ruby:2.6.8
    steps:
      - checkout
      - run: echo "A first hello"
      - run: sleep 25
  two:
    docker:
        - image: cimg/ruby:2.6.8
    steps:
      - checkout
      - run: echo "A first hello"
      - run: sleep 15
workflows:
    one_and_two:
      jobs:
        - one
        - two 
      





        
