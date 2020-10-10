---
layout: post
title:      "My breaking bad cli project"
date:       2020-10-10 17:01:24 +0000
permalink:  my_breaking_bad_cli_project
---


“*Never consider the possibility of failure; as long as you persist, you will be successful.*” – Brian Tracy



This project was a challenge. It could be frustrating at times, like learning any new thing I suppose, but piece by piece it came together. First the idea, then that idea becomes a flow chart. As planning comes to an end, you find yourself faced with a blank slate. Yours for the taking. It's a strange feeling, and the best way to learn in my opinion. 
I will layout the structure of my project, share some struggles and some code snippets, and try to sum up the journey this project took me on.

Starting out, I looked through lists and lists of API’s until I finally found the one that finally clicked. This Breaking Bad API gave me access to information on specific characters, episodes, or quotes. I ended up leaving quotes out of my project and focusing more on more functional character and episode objects.

### Planning and flow chart

##### The rundown

My basic idea was a program that lets a user fetch information based on characters or episodes. It would greet them somehow, take in some kind of input, use that to fetch the needed data from the API, and send that data to whichever class is needed to create the object. Then all it needed to do was display the information the user wanted and ask if they wanted to ask another question or exit!

You can use this link to see my initial flow chart, walking through the program described above:
https://viewer.diagrams.net/?highlight=0000ff&edit=_blank&layers=1&nav=1&title=BreakingBad.drawio#R7Vpdc5s4FP01fmyGb%2BzHxE26O5N2s5s2ndmXjgwyqBGIFXJs59evBMIICX8kxm7TqR8SdJFA3HN0z9WFkTvNVh8oKNKPJIZ45FjxauS%2BHznOxAv4X2FY1wbbC7zaklAUS1truEfPUBotaV2gGJadjowQzFDRNUYkz2HEOjZAKVl2u80J7t61AAk0DPcRwKb1K4pZKq22ZbUn%2FoAoSeWtx748MQPRY0LJIpf3GznuvPrVpzPQXEv2L1MQk6Vicq9H7pQSwuqjbDWFWPi2cVs97mbL2c28KczZIQM%2B4ofl1TP6NPn3ffItvP%2F87RP5%2Bk5iVbJ14w8Yc%2FfIJqEsJQnJAb5urVfVM0NxVYu32j63hBTcaHPjd8jYWmINFoxwU8oyLM%2BaM5cPU5IFjeQ8nJkHx7YzmVlO7I3D%2BTtJNDE%2FZZB81g%2BQZJDRNe9AIQYMPXXhBZIlyabfZugdQXwajiUZ7XkSL0lov8GvuQQDNIFMjmr9fUkpWCvdCtGh3H4fN%2FA79%2FECDb4989L684N6Bk1L8UlrqihRNb%2BUkP41%2By5WlGNhMIO4vqywS3wwiGDKlxOk3SWWg0w69wFQBGacFJV9J9FUsCQxFdIxuGJdjpSMkkc4JZhQbslJLpg3RxhrJoBRkvNmxLnEZ%2B5ePUHKEF%2Fel%2FJEhuK4ou0yRQzeF6Ai2JIHM0Fe3nuOq1WZ8n4w38VOcWW42sm95uy4i1VDoWUbYJoeqRJadKapZFVwVmHkTQXJ%2FoVvrCRJvCeAF1BFnSMCqOCsBYrCDAwY85i8zZMKdN34sAl7olER7WoTODUsa8ybKCwuNSc5uwEZwsKRD5DGIAfSLKPLuI8DA0DoaMvNNiF0eyB0Xw7hfrzs8dFRWoFnHwacApdCVzXbDRITriEVbel%2Fn7dhHjcjIgzKEkWfU5TXJ%2BQwu24pg3okoldKXkeKQxSmP06FMgepovxZpeilCuL4XQWxx%2F4xinBgwmAdzcVTZQz9eDrnSRvcUIsX%2FmFpw2C4OL9x6cMl1OK4HqBPDEvzmIrWgvJRSCzi%2BwRrUevukiz4roXnYegRVvufav9QHYOcsLTqhPJiwQyQWwjt%2FcoMZiXBCwYvaSQhraxtyzMCrjOMnHpaRtTkIIqchj1yGg4gpzvDvIIL925Z7VIhZChPDE%2BbflHT1RQUol%2B2SsQ2%2BUIklVHKZfIiRiXPpNdbwBkiU3E0GbCDC9O7QY939RA1nHcnvxOWEyQs2xJ5NVfZyfZTB1s9I%2FE0gtUPYwRbU0wtTUxlZvP6PfjQcX2zTNv4sRZVrBuD%2BD9qa9tdTgPEGXdsboG8YXaxB%2FrcNXyek1%2Fa5YGzdxN6XgQ8AwG4QqwuGGDuJ4ZIPpRwcgAylAMm8DmVdob%2BXgdvCsGqh4OTeTg4WjnPm8Zb51EW3%2B4CNT5vGu%2BEbwuW8Y9BxbHOC4v7xooR%2FplgmWivCg5cLS8tQOn38cNhC1BmIdSQH1NslijDoBJzBbIoRTi%2BBWuyEIjx7UD02LSuUkLRM0%2FFQZsstLsFx%2Br0uBcjJXN%2BiTK3%2FqZiYgpg0Lcx931%2FOytfXeg2iyXT2z%2B5YSo2aQdCvQO9rYnZVqLt9%2BP2Nzy9fttkGDtW8z8wYiBPxGu1l15e33ABzJnCcyh4JXh4kp1Q80AKaLLkUVaR7L8FLBkU1a0YMGCCeJ6qylaqHV5m2f9O72Sp4rYXEIrPWV0ulAXFAWqFP0dAOx43W0vx%2FeDCmyi%2F0ICxb2G54QlQNPezU07ukcOvZF0X9f%2B%2FF4RxYAOQCXzyWVnz24p%2B%2FpDoHhi07HAALdmVBisOvi9ghOaoikfShVZEIY%2BQ4ojIDyKOWTeD1di30uXwio1WjvPNsnBvyLL1NH4Qtpu1g8u7tyHuntVTT%2B9l8skq6uYnGzyB1wQ2wCKdnfEAEiTiqNZba05Jxv9VztadLPWVuwtgDDHhMpv1Vc5UphaQIv5QImB3B961J%2FaUx7orwq%2Fy5%2FrYunDcw1D0DkZx856kKwRBj4Db%2FiACzpvtd311otV%2BPOle%2Fw8%3D

It's pretty simple overall, I didn’t know My initial feelings on the flow chart but after building it out it felt nice to have a visual representation of My idea. 
Next, I’ll take you through my classes and how some things work behind the scenes.


### Now for the code

##### CLI

So first things first, the CLI class is like the glue that holds this application together. It gets the information from the user and sends it where it needs to go. And guess where does that data come when we successfully fetch it? Right back to the CLI Class, so it can print out the answer for the user! 
This part was a lot of fun for me, I’d have to say it was my favorite Class to build out of this program. Here is a small snippet to show you the layout of the code:

```
def start

puts ""
puts "Hello! Welcome to the Breaking Bad CLI App!"
puts ""
puts "You can choose to see information on characters, or episodes! Please enter which one you'd like to know more about!"
selection = gets.chomp.capitalize
first_option_choice(selection)
puts ""
puts "would you like to look for something else? input Yes or No."
@yes_or_no = gets.chomp.capitalize
if @yes_or_no == "Yes"
new_question = CLI.new
new_question.start_after_first
else @yes_or_no == "No"
puts "Thank you for using my Breaking Bad CLI!"
end
End
```

To get the output I needed, I split it into a few methods like this inside of the CLI class itself. This one runs first, but they mostly follow the same pattern. 
It interacts with the user by displaying greetings or prompts or telling the user what their input options are. I also used puts for spacing, which helped readability. It follows this pattern until we need to fetch data from our API! To use this I set a variable to the value of a` gets.chomp.capitalize`

I use gets to get a user input, .chomp removes the newline character from the end of the string, and .capitalize which turns the first letter capital, and makes the remaining characters lowercase. Then we send that variable with our user input over to another method to begin the process to get the users answer. Let's take a look into this first method `first_option_choice` method, which takes in the user input we just got!

```
def first_option_choice(selection)

    if selection == "Characters"
        puts ""
        puts "Please enter the name of the character youd like to learn about!"
        full_name
        name = @full_name
        name_info = API.fetch_characters(name)
        @char = Characters.all.find { |info| info.name == name.join(' ') }
        print_character(@char)
    elsif selection == "Episodes"
        puts ""    
        puts "Please enter the title of the episode you would like to learn about, or type list to see a list of episodes titles!"
        user_input_title
    else
      begin
        raise MyError.new "Input not found. Check your spelling, and remember to always capitalize the first letter!"
        rescue MyError => e
puts "~~~~~~~~~~~~~~~~~~~~~~~~"

puts e.message

puts "~~~~~~~~~~~~~~~~~~~~~~~~"

end
end
end
```

As soon as the user presses enter, our program routes their input here, where it triggers an if/elsif statement. It tests the user input, and depending on if it reads “Characters” or “Episodes” it will prompt the user for a second, more specific input and send the data to the appropriate class for object instantiation.
If the user input is not equal to either acceptable string, it triggers a custom error explaining some minor bug fixes to try, and then allowing them to try again.


##### API

The focus of the API class is to fetch the needed data and ONLY the needed data from the API. To do this, all three methods follow the same pattern but allow you to fetch a certain character or episode. In addition to being able to search by episode title, the user can also input “list” and they will be prompted to enter a season number, after which they will get a list of the episode names in the specified season. 
The user could then use that list to reference names or episodes they would like to look up.
Here is how I worked the methods out to fetch the necessary data:

```
def self.fetch_characters(name)
    url = "https://www.breakingbadapi.com/api/characters?name=#{name.first}+#{name.last}"
    uri = URI(url)
    response = Net::HTTP.get(uri)
    character = JSON.parse(response)
    character.each do |info|
        Characters.new(name: info["name"], char_id: info["char_id"], birthday: info["birthday"], occupation: info["occupation"],           nickname: info["nickname"], appears_in_seasons: info["appearance"], actor: info["portrayed"])
     end
end
```

##### Character and Episode

The Character and Episode classes are the simplest in the program, their only responsibilities are to initialize the objects for the episodes or characters our user would like to know about and store them.
```
def initialize(name:, char_id:, birthday:, occupation:, nickname:, appears_in_seasons:, actor:)
    @name = name
    @char_id = char_id
    @birthday = birthday
    @occupation = occupation
    @nickname = nickname
    @appears_in_seasons = appears_in_seasons
    @actor = actor
    @@all << self
end
```

I simply initialize with all of the data passed to us by the fetch_characters or fetch_episodes methods which both utilize .new to send the initialization data. Then I store all of the objects in a @@all class variable that is set to an empty array.


##### Afterthoughts
Leading up to the project, I felt like I had a good grasp of ruby. Beginning the project made me understand that the knowledge I had at the time was good, but not enough for the task at hand. I felt like I had been given the right tools, and Just like any set of tools they don’t do much good until you get in there and use them. It takes the hands-on work. Coming out of the other side came with a feeling of accomplishment and deeper understanding of the concepts used.


