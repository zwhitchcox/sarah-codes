## Intro

I am a self-taught code bear, meaning that I did not go to school for it or have any formal training at all. This meant I had to learn to be resourceful and use the web as my teacher. This is a valuable skillset in and of itself and one that I still rely on every day.

So, as you progress through these modules, try to look stuff up on your own. It may take you down a different path, but don't be afraid of going down rabbit holes. A wide breadth of knowledge to draw from will help you to become a better coder.

### How Software Works

Well, I would highly recommend your read the book [code](https://www.amazon.com/Code-Language-Computer-Hardware-Software/dp/0735611319) by Charles Petzold, but in a nutshell...


#### Electromagnetism

Electricity is simply the movement of electrons through a given medium, and electricity and magnetism are inter-related. Combined, form the force, "electromagnetism". If you have a wire surrounded by the north pole of a magnet on one side and the south pole of a magnet on the other side, and spin the magnet around the wire, you will induce a current, which just means make electrons flow through the wire.

Similarly, if you pump electrons through the wire, you can make the magnet spin around.

If the magnet is moving as a result of electricity, you have created an electric motor. If you are spinning the magnet around the wire and generating electricity, you have created a generator.

This is how a windmill works, by spinning the magnet to generate electricity. A dam works the same way; as water falls, it spins a turbine around a wire, producing power.

Similarly, an electric motor works by pumping electrons through a wire, causing a magnet to spin.

This is the fundamental concept that makes virtually all of our modern technology work.

#### Batteries

We can store the power we generate with a battery.

A battery has two terminals, a "positive" terminal and a "negative" terminal. These terminals are connected to a collection of ions. The positive terminal is connected to the positive ions, and the negative side is connected to the negative ions.

A negative ion is an atom with extra "loose" electrons, and a positive ion is an atom with extra "holes" for electrons to fill.

If a positive ion and a negative ion are near each other, the extra electrons from the negative electron can jump to the positive ion, thus restoring equilibrium. Nature does not like high concentrations of energy (see Newton's law of entropy). In fact, the inevitable "heat death" of universe refers to a time when all energy is evenly distributed. With all energy evenly distributed, nothing will have a need to "move", thus constituting the "death" of the universe. But I digress.

We can connect the two terminals of the battery with a wire, and electricity will flow from the positive ions to the negative ions.

Wires are typically made of copper, because the can readily accept or give up electrons due to its molecular structure. This means it makes a good "middle man" between the different collections of ions. It can easily transfer the electrons between a source and the destination.

So, on one end of the wire, the positive ions take free electrons from the copper atoms, and on the other end, the negative ions have an excess of electrons which the give to the coppper atoms

If we run this wire through a motor, we can cause it to spin. If we run it through a light bulb, we can produce light. If we run it through a series of logic gates...

#### Logic Gates

If electricity is run through a wire and comes to a fork, it will go the path of least resistance. So, if one path is very narrow, and the other path is very wide, more electrons will flow through the wider path. If one of the paths is disconnected completely, all electricity will flow down the other path

Let's say we have a button connected to the power source of a magnet. When the button is down, the magnet is turned on, and the electricity goes down one path. Let's call that path "1". Let's call the other path, path "0".

```
                            -----path 0-----------------
--------wire 1-------------/
                            -----path 1--------------------
battery + -----button-----magnet
battery - ---------------------|
```

When we press the button, the magnetism pulls the wire down, and the path switches:

```
                            -----path 0-----------------
--------wire 1-------------
                           \-----path 1--------------------
battery + --button (down)--magnet
battery - ---------------------|
```

So, formally, we can say

```
if (button is down) then (path 0 is on)
if (button is down) then (path 1 is off)
if (button is up)   then (path 0 is off)
if (button is up)   then (path 1 is on)
```

Let's just call "up" `1` and "down" `0` and "on" `1` and "off" `0`.

That gives us

```
if (button is 0) then path 0 is 1
if (button is 0) then path 1 is 0
if (button is 1) then path 0 is 0
if (button is 1) then path 1 is 1
```

That's a little confusing though, so lets join path and its number together:

```
if (button is 0) then path0 is 1
if (button is 0) then path1 is 0
if (button is 1) then path0 is 0
if (button is 1) then path1 is 1
```

You'll notice `path0` is just the opposite of `path1`. So, really, we can just refer to these paths as `wire`, and we'll let `wire = 1` mean `path1 = 1` and `path0 = 0`, so:

```
if (button is 1) then wire is 1
if (button is 0) then wire is 0
```

Really, though, this simplifies to

```
wire = button
```

or "wire is whatever button is".

But let's remember, that `button` could change at any time, so we need to loop through this logic and constantly re-evaluate:

```
loop {
  wire = button
}
```

We'll start out with both `wire` and `button` being `0`

```
wire = 0
button = 0
loop {
  wire = button
}
```

Let's connect a light bulb to path 1, so

```
bulb = wire = button = 0
loop {
  bulb = wire = button
}
```

You can see that out input is the button and our output is the light bulb. You can imagine the button as part of a keyboard and the bulb as part of a monitor. These are the fundamental building blocks of a computer.

Now, let's do something wacky. Let's connect the output "path 0" to the magnet controlled by the button. So, now, every time the loop is re-evaluted, if "path 0" is "on", it will pull the magnet down and turn on "path 1", which will then cut the power and turn on "path 0" again, which will turn "path 1" back on. So, essentially it toggles the output of `wire`:

```
bulb = wire = button = 0
loop {
  wire = the opposite of whatever it was before
  bulb = wire or button
}
```

You can imagine the light bulb flickering on and off.

If instead of a wire, we had a hammer, and two bells on either side, the hammer would go back and forth ringing the bells. This is how old telephone ringers used to work.

If there were a weight instead of a wire, you could imagine the weight going back and forth. This is how your cellphone vibrates, carrying on the tradition of its ancestor.

But I digress.

Let's say instead of that, we hook the output of path 1 to the magnet that the button controls. Now, if we press the button, the light bulb stays on.

```
bulb = wire = button = 0
loop {
  if (button is 1) then (wire = 1)
  if (wire is 1) then (bulb is 1)
}
```

Here we can see that the `=` sign means we're *setting* wire to `1`, and `button is 1` means we're checking to see if it's already `1`.

So, as we loop through, we can see that if `button` is `1`, we set `wire` to `1`. If `wire` is `1`, then `bulb` is `1`. Once `wire` is `1`set, there is no changing it. Let's abbreviate `button is 1` to just `button`, so:

```
bulb = wire = button = 0
loop {
  if (button) then (wire = 1)
  if (wire) then (bulb)
}
```

This is similar to how a real programming language is written.

The point is that we can adjust what the code is doing by changing the underlying circuits. These circuits are called "logic gates", and it's how a computer is made. There are logic gates to

* invert an output (change it to the opposite of whatever was input)

```
if (input) then (output = the opposite of input)
```

or, simplified

```
output = the opposite of input
```

* output a 1 if either of two inputs are 1, otherwise 0

```
output = input1 or input2
```

* output 1 only if two inputs are both 1

```
output = input1 and input2
```

* output if one and only one of inputs is 1

```
output = input 1 exclusive or input 2
```

This is called "boolean" logic, and if you were to look at what the silicon was doing with a microscope, and that were possible, you could break everything it's doing down into one of these four actions.

#### Boolean logic

Now that we know what the circuits are doing, let's build some logic on top of that.

But first, let's go over some symbols:


**INVERT**

`~` means "INVERT", so for

```
output = ~input
```

if `input` were `0`, `output` would be `1`
if `input` were `1`, `output` would be `0`


**OR**

`|` means "OR", so for

```
output = input1 | input2
```

|---------------------------
|input 1 | input 2 | output |
|---------------------------|
|   0    |   0     |   0    |
|   1    |   0     |   1    |
|   0    |   1     |   1    |
|   1    |   1     |   1    |
|----------------------------

**AND**

`&` means "AND", so for

```
output = input1 & input2
```

|---------------------------
|input 1 | input 2 | output |
|---------------------------|
|   0    |   0     |   0    |
|   1    |   0     |   0    |
|   0    |   1     |   0    |
|   1    |   1     |   1    |
|----------------------------

**XOR**

`^` means "XOR", so for (exclusive or)

```
output = input1 ^ input2
```

|---------------------------
|input 1 | input 2 | output |
|---------------------------|
|   0    |   0     |   0    |
|   1    |   0     |   1    |
|   0    |   1     |   1    |
|   1    |   1     |   0    |
|----------------------------

With these tools, we have the building blocks of "boolean algebra", named after George Boole who invented it before computers even existed.

#### Bits

They operate on 0s and 1s only, which is good, because we only have an "on" or "off state for a circuit, but by composing them, we can add, subtract, divide, do anything a computer can do.

A base 2 digit is called a "binary digit" or a "bit". By composing bits we can represent numbers higher than `0` or `1` though.

Binary numbers are just like regular numbers, only they only have two digits. So, counting in binary, would go like

```
0
1
10
```

What's that? Why did I skip to ten? Well, `10` in binary form is actually `3` in decimal. See, with decimal number (or base 10), we only have digits 1-9, so when we run out, we have to add another digit, so counting goes

```
1
2
3
...
8
9
10
```

See, we rolled over after `9`. Now, we're just rolling over after the `1`. So, we can keep counting:

```
0
1
10
11
100
101
110
111
```

That was 0 through 7. That is 8 total numbers with just 3 binary digits. You'll notice the maximum number is 2 to the power of whatever the number of digits are.

This is just like in decimal format. Excepted it would be 10^(number of digits). So, with 3 digits in decimal, the maximum amount of numbers is 10^3, or 1000. This is true, because the maximum number is 999. Add 0 and that's 1000.

To computers, everything is represented in binary format, so they have to be able to add subtract, multiply and divide using just our boolean operations. These are called "bitwise operations" in programming-speak.

#### Bitwise Addition

So, how can we add? Let's see. If we have two numbers, `010` and `110`, we can add them together, just normally, like

```
  010
+ 110
 1000
```

Notice that we carry after `1` instead of `9`, because `1` is our maximum digit just like `9`.

But remember, we only have bitwise operations. So, how do we do this with just bitwise "OR" "AND" "XOR", and "INVERT" operations?

We would compare the first numbers, `0` and `0`. We would `^` them together for the least significant bit of our output and get `0`. This is because if both are `0`, the first bit of the answer will be `0`. If both are `1`, then the first bit will also be `0`, because we carry the `1`. It's only if only one of the bits is `1` and the other is `0` that the answer bit will be `1`. This is exactly the `^` operation.

Next, we need the "carry bit". That's simple. We only have a carry bit if both the digits are `1`. So, we use `&`.

Altogether, that's

```
sum bit: input1 ^ input2
carry bit: input1 & input2
```

Now, but for the next digit, we actually have 3 numbers, the previous carry, `input1`, and `input2`...so how do we add 3 numbers together?

```
sum bit: (input1 ^ input2) ^ carry input
carry bit: ((input1 ^ input2) & carry input) | (input 1 & input 2)
```

Now, the sum bit is `1` if *only* one of `input1`, `input2`, or `carry` was `1` or all three were `1`. Because

if all three were `1`, then there is one to carry and one left over.

if only one were `1`, there is no carry,

The carry bit is true if any two of the `input1`, `input2`, and `carry input` were true. That is simply the boolean way of saying that.

Now, we have the sum bit and a new carry bit. We plug that carry bit into the next two numbers and keep going until we have get to the end.

#### Bitwise Subtraction

Subtraction is a bit more difficult. Really we can only add in bitwise operations, but there is a hack we can use to represent numbers as "negative" and then add them to fake "subtraction".

Computers actually represent the number `0` as `00000000`. An 8 digit binary number is called a "byte", sort of a play on `bit`. So, a byte is 8 bits long. But, there are no negative numbers, so it represents `-1` as `11111111`.

But, if we add `1` and `-1` in binary, we would get

`11111111` + `00000001`. This results in an integer overflow. This means that there was a carry bit leftover when we added the two integers. If there is a carry bit leftover, the computer disgards it. So, adding these two numbers would give us `00000000`, which is the exact right answer (`1 + -1 = 0`)

to get `-2`, we still subtract `1` from `-1`, so we would get `11111110`. Add this to `00000010`, and we still get `0` (`-2 + 2 = 0`). You can play with this an convince yourself, because it's counter intuitive, but it works out.

#### Other Operations

Not going to go into everything, but essentially, with multiplication, You just keep a counter and add the same number over any over again decrementing the counter each time until it gets to 0. Same thing for division, but it's backwards.

These operations are built into the silicon of computers. They're the fundamental operations we use to do everything a computer does.

#### Assembly

Your computer uses the above operations to run every program a modern computer can. Different operations are represented by different codes. To write these codes, you use a language called "assembly". Assembly tells the computer when to add/subtract/multiply/divide, but it can also control the flow of operations.

So, you would give the computer a list of instructions, and it would go through them one at a time. As the computer goes through the instructions, it stores numbers its using in registers. So, an instruction might say load the value of register 6 into the instruction register. The value of register 6 might've said to add the values of register 8 and register 9.

Since you can load an arbitrary instruction and execute it, this means you can have a computer run in a loop if you want, and that's how computers work. You give them an instruction set that it constantly loops through and tells it what to execute. The circuits on which all this is executing is called the "CPU", and it's the brain of your computer.

If the CPU is looping through the instructions you write, you can tell it to listen for events like a key being pressed or a monitor being plugged in. These events are sent to the CPU and loaded into registers through "buses", which are essentially just "wires" from other devices plugged into your computer. These can flip bits in the to set a number to send it data. The data could be an instruction itself, which the CPU could execute.

Of course, you can have multiple CPUs talking to each other through these buses too, or they could all be integrated into the same circuit, in which case they would be different "cores" of the same CPU. This allows computers to be really fast. A supervisor manages all the different actions of the CPUS to make them all work togther.

The assembly language which contains the instruction set is "compiled" or converted into machine language. Machine language contains the raw instructions for your computer to execute. Different CPUs can have different instruction sets. A popular instruction set is x86, which has 86 instructions the CPU knows how to execute.

Another popular CPU type is ARM, which doesn't have as many instructions, but gives you more flexibility with what you can do with the registers.

Still though, you'll probably never write a line of assembly. You will write a higher level language which will be converted to machine code. These languages have "compilers" which are convert the language to machine code for you. It's unlikely you will care about which register is doing what. The instruction you might send would be "add these two numbers". It doesn't really matter how the CPU does it.

#### The OS

Even with higher level languages, you're still not going to execute machine language directly. Otherwise, you could say, "get Janey's password and give it to me". Your programs send instructions to the operating system, which execute them for you and decides if you are allowed to excute them.

There are different levels of privileges. An administrator can do anything that the OS allows him to, including create other users and administrators. This is called "privileged access". Still though, the operating system is receiving requests and executing them. The OS has it's own set of resources that the administrator can't access that run the fundamental operations of a computer, like talking directly to the CPU.

The core operations of an OS are performed by the kernel. The most famous kernel is called "linux". It is open source, meaning anyone can look at the code it is executing and/or adjust it to fit his needs. He can also send in patches to fix something that is wrong with the source code or add functionality. Open source projects are also typically free to use.

There are a variety of operating systems built on top of the linux kernel.

But there are two other popular operating systems known as Mac OS X and Windows. These OS's kernels are named "darwin" and "MS-DOS". They were created in the 80's, and their code is proprietary, meaning no one can see it, and you have to pay to use it.

#### Software

So, now we know how computers work, we are ready to learn how to write code for them to execute. You won't really need all the above information in your day-to-day life, but it is helpful to understand the full context of what you are doing, because things will make more sense. This will make it easier to learn.

One of the jobs of the OS is to manage processes. The software you write will generate these processes which will run the instructions you give it. These processes could read/write files, communicate with other computers, play music, etc. Anything a computer is capable of.