# The Linux Kernel Mentorship Program (LKMP)

## Academic Background

I initially started programming when I was about to finish high school. Thanks to COVID, I suddenly had a lot of free time, and I ended up using it to build a simple chatbot (not the AI chatbots as we know them today; this was before ChatGPT) for moderation and entertainment commands on Discord. By the time COVID was over, I had started my Diploma in Computer Technologies, where I explored a wide range of topics and spent the next 2~3 years learning game development. This helped me build a solid understanding of OOP, graphics programming, event handling, and related concepts.

I was introduced to operating systems fairly late, during the final (3rd) year of my diploma, around the same time I picked up an elective in advanced computer networking. I completed my diploma in 2024 with the honor of being a gold medalist (the Indian equivalent of a valedictorian; ranked #1 across my college for the duration of the diploma) and ranked within the top 100 graduates across the state.

Following this, I began my undergraduate studies at Pune Institute of Computer Technology in the same year. The college has several active student-led organizations and clubs, and I've been actively involved in the Game Dev Community and the ACM Student Chapters. Around this time, however, I realized that while I enjoyed game development, it was more of a hobby than a long-term career option. I wanted to work in a domain that genuinely interested me.

I began exploring different areas and, by early 2025, arrived at systems programming. I spent the last four months of my second year of undergrad building a platform-independent assembler with my own ISA, which gradually evolved into something resembling a primitive, stack-based version of LLVM. This eventually led to a conference paper that was published in IEEE, and I'll be presenting it at the ICEI conference on January 9, 2026.

Because of this growing interest, I also started becoming more active in compiler and open-source communities. I recently built a compiler on top of the same project as part of a week-long hackathon organized by IICT (Innovations in Compiler Technology), Bengaluru. When I first joined the college, its Open Source Community was still in a very early stage (it has recently crossed 800 members!). The community has several active members who regularly share news, updates, and opportunities in the open-source space. LKMP was one such opportunity that I discovered through them.

## Beginning

Having just completed a fairly large project and entering my third year, I started becoming more active within the PICT Open Source Community. I listed my project under GirlScript Summer of Code and acted as a project admin there from August to November 2025. In July 2025, the community conducted an "Intro to Open Source Programs" session, where I first learned about LKMP.

Prior to this, I had little to no experience working on community-organized projects, especially at this scale. I'd strongly suggest spending time on the suggested course, particularly to understand how patches are submitted and accepted, and how the community functions overall. It contained several extremely useful guidelines that I've found myself referring back to while submitting patches.

While completing the prerequisite tasks, I decided to properly organize what I had done and the problems I faced. I won't be sharing what I submitted (do it yourself :D), but some of the issues I ran into are worth mentioning.

### Working with Syzkaller

The first time I used Syzkaller was to run `decode_stacktrace.sh` on [this report](https://syzkaller.appspot.com/bug?extid=240906f6485cdb6035a7). The task itself wasn't particularly difficult, but I ended up wasting time recompiling the kernel. In hindsight, it would have been much better to simply use the files that were already provided in the report.

Seriously, **know what information is available to you, and work with it.**

### Working with VirtualBox

One simple but annoying issue I faced with VirtualBox was that the recompiled kernel booted successfully… but didn't accept any mouse input, and VirtualBox kept showing an error message (specifically, "The VirtualBox kernel service is not running.").

After some digging, I found out that the essential VirtualBox modules weren't enabled in the kernel config. If you're working with VirtualBox, don't forget to set the following options to `m`:

- `CONFIG_DRM_VBOXVIDEO`
- `CONFIG_VBOXGUEST`
- `CONFIG_VBOXSF_FS`

### Working with printk

At one point, I was trying to print messages when loading and unloading kernel modules of my own creation, but I ran into a very strange issue. The messages appeared in reverse order: "Bye!" was printed on module insertion, and "Hello, World!" showed up on module removal.

After a bit of debugging (okay, maybe a few hours), I realized this was entirely on me. I didn't fully understand the functions I was calling, and a missing `\n` at the end of the message caused the log buffer to flush incorrectly. So yes, **know your tools** (or, in this case, your functions).

### Other Errors

While working on Linux Mint, I spent an embarrassingly long time trying to capture kernel panic logs. After a lot of head-scratching, I finally came across [this discussion](https://forum.linuxfoundation.org/discussion/868772/how-to-capture-the-panic-message) on the LFX Mentorship forum.

Moral of the story: **refer to the forum if you're facing an issue, chances are, someone else already has** (insert apes_together_strong.jpg).

## Office Hours

The program runs in both summer and fall, and is led by Shuah Khan along with one or more co-mentors. For the summer cohort, you can choose between a part-time, six-month option or a full-time, three-month option. For the fall cohort, however, it's strictly full-time.

The program itself is fairly hands-off, with a weekly one-hour guidance and doubt-resolution session. Some points from these sessions that I found particularly important were:

- As mentioned earlier, know what information is available to you. Once accepted, you'll likely get access to a Google Drive with all the necessary resources.
- Choose at most two subsystems to contribute to. The kernel is huge, and it's important to narrow your focus.
- Keep track of the process you use to find bugs, along with any tests you run (tests are necessary for any logical changes, i.e., code changes).
- Run `checkpatch --strict` before sending patches.
- LFX mentorship is a one-time opportunity; you can only participate in one mentorship and can't join another after completing it.
- "Meaningless patches" don't count. Examples include translating between dialects of English or simple spell fixes.
- All other kernel-directed patches count, even those sent before the mentorship officially starts (there's probably a limit to how old a contribution can be, but patches sent during prerequisite tasks do count).
- Use an imperative tone in patch descriptions (this is mentioned in the prerequisite course, but still worth emphasizing).
- If you lack the necessary conditions for testing (such as missing hardware), it's better not to attempt that particular issue.
- Learn how to write good commit messages. Focus on _what is fixed_ and _why it's fixed in that way_, rather than just _what was changed_.

## Choices Available

As mentioned above, it's recommended to choose the subsystems you want to contribute to. You can refer to the subsystem APIs section in the kernel documentation to decide which areas interest you. When working with kernel code, you need to be careful, any accepted change will eventually be rolled out to millions of devices. As a result, code changes require a very rigorous level of testing.

Considering the time I had available while balancing academic exams, interviews, and other commitments, I decided to contribute to documentation for now, with plans to return to code contributions once I have more time. Fortunately, the kernel provides several useful scripts to help with this (Documentation Patches). I initially started by using available spellcheck tools to detect spelling errors and sending spell-fix patches. While these don't count toward the mentorship, they did help me get comfortable with the patch submission process.

I later used `make refcheckdocs` to find dead links in the documentation. Once I found one, I checked lore to identify the exact commit that introduced the issue (the commit hash should be referenced when submitting the patch). This often helped me locate the correct link, since in most cases files are renamed or moved rather than deleted outright. The fix itself is usually straightforward, but such issues aren't very common.

In the long run, it makes more sense to focus on code patches. I plan to start working on those after my exams. Fortunately, gaining experience in storage-related kernel programming should be helpful for my internship in the summer of 2026, so I already have a rough idea of what I want to focus on. I’ll update this blog once I get started.

As of now, the status of my patches is as follows:

- 3 spell-fix patches applied to the main branch
- 3 spell-fix patches reviewed/acked but not yet applied
- 6 spell-fix patches where a duplicate patch was already merged
- 3 spell-fix patches with no response

- 2 patches applied (one in `linux-next` and another in `docs-next`)
- 4 patches pending review
- 1 patch where a duplicate was merged
- 1 incorrect patch
