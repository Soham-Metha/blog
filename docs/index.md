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
- keep a track of the process used to find bugs, as well as any tests performed (tests are necessary in case of any/all logical changes(i.e. code changes))
- run checkpatch --strict before sending patches.
- LFX mentorship is a one time opportunity, you can only ever be in 1 mentorship; can't join another one even after the current one is completed.
- "meaningless patches" don't count, examples of such patches are translation from one dialect of english to another, or spell fixes.
- All other patches directed towards the kernel count, even those submitted before the mentorship started (well, i guess there should be a limit to how old of a contribution counts, but atleast those patches you sent when completing the pre-requisite tasks count).
- Use imperative tone in the patches ( i am aware this is mentioned in the pre-requisite course, but still an important reminder)
- If you lack the necessary conditions (such as missing hardware) for testing, then it's suggested to not attempt that specific problem.
- Learn how to write good commit messages, try to focus on "what is fixed" and "why is it fixed in this way and not some other way" instead of "what was changed in the code".

## Choices available

 As stated above, It is suggested to choose the subsystems you want to contribute to, you can refer the subsystem APIs kernel doc page to know what part you want to contribute to. When working with code in the kernel, you need to be quite careful as any change you make will (if accepted) eventually be rolled out to millions of devices. As such, a very rigorous amount of testing is needed for code changes. I considered the time I had on hand while balancing academic exams, interviews, etc and ended up choosing to contribute to the Documentation for now, and planning to return to the coding parts once I have the time. Fortunately for me, The kernel included some very useful scripts. I initially started contributing by using readily available spellcheck tools to detect spelling errors and sending spell fix patches, although they don't count, they did help me familiarize myself with sending patches.

 I then used 'make refcheckdocs' in order to find various dead links. Once found, I checked the lore to find the exact commit that introduced the issue (it's commit hash should be referenced when submitting the patch), this usually helps me find the correct link as well, as in most cases, the files are renamed/moved instead of being removed completely. It's a fairly simple fix after that, but such fixes are quite rare. It's better to focus on code patches, I plan on starting work on them after my exams, fortunately for me, having storage-related kernel programming experience will be helpful to my internship later in summer 2026, so I have an idea of what to focus on. I will update more info on this blog once I start. Currently, the status of my patches is as follows:

 3 spell fix patches applied to the main branch
 3 spell fix patches that have been reviewed/acked but not applied
 6 spell fix patches that have had a duplicate patch merged already
 3 spell fix patches without any response

 2 patches applied, one in linux-next and another in 
 4 patches to be reviewed
 1 patch which has a duplicate patch merged
 1 incorrect patch
