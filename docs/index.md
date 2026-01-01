# The Linux Kernel Mentorship Program (LKMP)

## Academic Background

 I initially started programming when I was about to complete my high school, having all the free time I needed thanks to COVID, I started by creating a simple chatbot(Not the AI chatbots as we know them; this was before ChatGPT) for moderation and entertainment commands on Discord. By the time Covid was over, I had started my Diploma on Computer Technologies where I explored various topics and spent the next 2~3 years learning game development, which allowed me to establish a good understanding of OOP, graphics programming, event handling, etc. I initially learned about operating systems in my final (3rd) year there, I also picked up an elective in advanced computer networking at the same time. I completed the diploma in 2024 with the honor of being a gold medalist (Indian equivalent of Valedictorian; Ranked #1 across college for the duration of the diploma) and ranked within top 100 among all grads across the state.

 Following this, I started undergrad studies at Pune Institute of Computer Technology in the same year. The college has quite a few active student-led organizations/clubs (of which I am active in the Game Dev Community and ACM Student Chapters). By this time, however I realized that Game Development was more of a hobby for me; not a career option, I wanted to choose a domain that truly interested me. I started exploring various domains and finally, as 2025 started, I arrived at the conclusion of Systems Programming. I spent the last 4 months of my 2rd year (of undergrad) creating a platform independent assembler, with my own ISA, which ended up becoming something like a primitive version of a stack-based LLVM (I ended up writing a conference paper on this, published in IEEE and will be presenting on this at the ICEI conference on 9th Jan 2026).

 Due to this interest I also began being active in various compiler and open source communities. I ended up creating a compiler on top of my project recently as a part of the week-long hackathon organized by IICT (Innovations In Compiler Technology), Bengaluru. When I joined the College, it's Open-Source Community was just budding (Recently crossed 800 members!). They have quite a few active members who periodically share the latest news, advances and opportunities in the Open Source Community, LKMP was one such opportunity I found there.

## Beginning

 Having Just completed a huge project, entering into 3rd year, I started by becoming active within the PICT OSS Community, listed my project under the GirlScript Summer of Code, acting as a project admin there from August to November 2025. In July 2025, The Community held a "Intro to Open Source Programs" session where I learned about LKMP. Prior to this I had little to no experience working on community-organized projects (especially one of such a large scale). I'd suggest focusing on the suggested course quite a bit, understanding how patches are submitted and accepted, how the community functions. It contained quite a few extremely useful guidelines which you may find useful to refer to when submitting patches. While completing the pre-requisite tasks I decided to properly organize what I have done & problems faced, of which I won't be sharing what I submitted (Do it yourself :D). Various problems I faced were :

### working with Syzkaller

 The first time I used Syzkaller was to use decode_stacktrace.sh on [This report](https://syzkaller.appspot.com/bug?extid=240906f6485cdb6035a7), which itself wasn't difficult, except that I wasted time re-compiling the kernel, it would've been better to just use the files which were directly provided in the report. Seriously, **Know what information is available to you, and work with it.**

### Working with VirtualBox

 A simple problem I faced with VirtualBox was that the recompiled kernel booted successfully, ... but it didn't accept any mouse inputs and VirtualBox showed an error message. (Specifically, "The VirtualBox kernel service is not running."). After a bit of googling around, I found out that the Essential VirtualBox Modules were not set within the config file. If you are working with VirtualBox, Don't forget to set the following to 'm'

- `CONFIG_DRM_VBOXVIDEO`
- `CONFIG_VBOXGUEST`
- `CONFIG_VBOXSF_FS`

### Working with printk

 At some point in time, I was trying to print messages when loading/unloading modules of my own creation, but I faced a very weird issue, messages appeared in reverse order; "Bye!" printed on module insertion and "Hello, World!" on module removal. After a bit of debugging (well, may have been a few hours? ), I learned that it was because I didn't understand the functions I was calling, a missing '\n' at the end of the message caused the log to be flushed incorrectly. So yes, **know your tools**(or in this case, functions.)

### Other Errors

Working with Linux Mint, I spent an embarrassingly long time trying to capture the panic logs. After a lot of head scratches, I found [this discussion](https://forum.linuxfoundation.org/discussion/868772/how-to-capture-the-panic-message) on the LFX Mentorship forum. So, **Refer the forum, if you are facing an issue, chances are, someone else also did**, (insert apes_together_strong.jpg).

## Office Hours

 The program runs in summer as well as fall; led by Shuah Khan with one or more co-mentors. For those applying in Summer, you have the choice to work part time for 6 months, or full time for 3. For the Fall option, the part time is no longer a choice, it is a full time only program.
 The program is quite hand-off, having an hourly guidance/doubt resolution session once a week. Some points from these sessions that I found very important are:

- As said previously, know what information is available to you, once you are accepted, you will probably get a google drive containing all the necessary resources
- Choose atmost 2 subsystems you want to contribute to, the kernel itself is quite large, it's important to know what you want to focus on.
- keep a track of the process used to find bugs, 