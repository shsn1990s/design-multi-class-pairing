{{PROBLEM}} Multi-Class Planned Design Recipe
1. Describe the Problem
As a user
So that I can record my experiences
I want to keep a regular diary

As a user
So that I can reflect on my experiences
I want to read my past diary entries

As a user
So that I can reflect on my experiences in my busy day
I want to select diary entries to read based on how much time I have and my reading speed

As a user
So that I can keep track of my tasks
I want to keep a todo list along with my diary

As a user
So that I can keep track of my contacts
I want to see a list of all of the mobile phone numbers in all my diary entries

2. Design the Class System
ExcaliDraw Diagram: spec/diaryandtodos.excalidraw

Also design the interface of each class in more detail.


class Diary
  def initialize
  end

  def add(entry)
  end

  def list
  end

  def read(entry)
  end

  def read_time_limited(wpm, mins)
  end
end

class DiaryEntry
  def initialize
  end

  def title
  end

  def contents
  end

  def reading_time
  end

  def extract_number
  end
end

class Contacts
  def initialize
    # ...
  end

  def add(number)

  end

  def list
    # Returns a list of contacts
  end
end


class TodoList
  def initialize
  end

  def add(task)
  end

  def list
  end
end

class Task
  def initialize
  end

  def title
  end
end

3. Create Examples as Integration Tests
Create examples of the classes being used together in different situations and combinations that reflect the ways in which the system will be used.

# EXAMPLE

# Add and entry to a new diary

diary = Diary.new
entry = DiaryEntry.new(title, contents)
diary.add(entry)
diary.list => [entry]

# Add an entry to a diary which isn't empty

diary = Diary.new
entry = DiaryEntry.new(title, contents)
entry2 = DiaryEntry.new(title2, contents2)
diary.add(entry)
diary.add(entry2)
diary.list => [entry, entry2]

# Read the only entry from a diary

diary = Diary.new
entry = DiaryEntry.new(title, contents)
diary.add(entry)
diary.read(entry) => entry

# Read an entry from a diary that contains multiple entries

diary = Diary.new
entry = DiaryEntry.new(title, contents)
diary.add(entry)
entry2 = DiaryEntry.new(title2, contents2)
diary.add(entry2)
diary.read(entry2) => entry2

# Read a time-limited entry from the diary within the word count
diary = Diary.new
entry = DiaryEntry.new(title, word * 50)
diary.add(entry)
read_time_limited(50, 1) => entry

# Return empty list if no entry from the diary within the word count
diary = Diary.new
entry = DiaryEntry.new(title, word * 100)
diary.add(entry)
read_time_limited(50, 1) => []

# Read a time-limited entry from the diary - selects longest time limited entry within the word count
diary = Diary.new
entry1 = DiaryEntry.new(title, word * 50)
entry2 = DiaryEntry.new(title, word * 100)
entry3 = DiaryEntry.new(title, word * 150)
diary.add(entry1)
diary.add(entry2)
diary.add(entry3)
read_time_limited(100, 1) => [entry2]

# Extracts a single phone number from the contents of diary entry
entry = DiaryEntry.new(title, "New number is 07000000000")
contacts = Contacts.new
contacts.add(entry.extract_number)
contacts.list => ["07000000000"]

# Extracts two phone numbers from the contents of diary entry
entry = DiaryEntry.new(title, "I can be contact on 07000000000 or 07000000001")
contacts = Contacts.new
contacts.add(entry.extract_number)
contacts.list => ["07000000000", "07000000001"]

# Adds a single task to an empty todolist
todolist = TodoList.new
task = Task.new("title")
todolist.add(task)
todolist.list => task

# Add a task to a non empty list
todolist = TodoList.new
task1 = Task.new("title 1")
task2 = Task.new("title 2")
todolist.add(task1)
todolist.add(task2)
todolist.list => [task1, task2]

4. Create Examples as Unit Tests
Create examples, where appropriate, of the behaviour of each relevant class at a more granular level of detail.

# EXAMPLE

# Constructs a diary

diary = Diary.new
diary.all => []

# Constructs an entry

entry = DiaryEntry.new(title,contents)
entry.title => title
entry.contents => contents

# Calculates reading time based on number of words
entry = DiaryEntry.new(title, word * 200)
entry.reading_time(100) => 2


# Calculates reading time rounding up number of minutes
entry = DiaryEntry.new(title, word * 250)
entry.reading_time(100) => 3

# Constructs a TodoList
todolist = TodoList.new
todolist.list => []


5. Implement the Behaviour
After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour.