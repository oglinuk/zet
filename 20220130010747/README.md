# Why Backups and Integrity Checks are Important

My personal experience of data loss was a final assessment for one of my
classes during my time studying. This was during my early days of using
Linux and LibreOffice.

Can't remember what exactly happened, but the document became corrupt and
unaccessible. With no backup, I had to restart the assessment from
scratch.

This event is what lead me to discover the `rsync` tool, since I didn't
want to rely on a proprietary piece of software for making backups.

While browsing reddit, I glanced a post that was titled "Linus Tech Tips
lost a lot of data... Again" from `/r/sysadmin`. While I don't normally
watch Linus Tech tips, I am always interested to learn from someone elses
mistake. Watching the video made me remember my experience and showcases
why ***it is so important to have data backups and integrity checks in
place***.

I encourage you to take a moment and think if any of your devices (your
phone, laptop, desktop, tablet, or whatever) died in the next 10 minutes,
what data would you lose forever.

There are plenty of good tools out there like `rclone` if you don't want
to use plain old rsync.

Related:

* Linus Tech Tips: Our data is GONE... Again
	<https://www.youtube.com/watch?v=Npu7jkJk5nM>
* `man rsync`
* rclone
	<https://github.com/rclone/rclone>

Tags:

	#data #backups #integrity #data-loss
