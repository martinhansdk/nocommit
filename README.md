# nocommit
A commit hook to prevent accidental commits

Go to start of metadata
We have a pre-commit hook in our Subversion server which makes subversion reject any file that contains the string NOCOMMIT (case insensitive, so nocommit will work too). Here is a little demo:
    bash /tmp/xyz/workspace> echo "NOCOMMIT" >>  main.cpp
    bash /tmp/xyz/workspace> svn commit -m "test commit"
    Sending        main.cpp
    Transmitting file data .svn: Commit failed (details follow):
    svn: 'pre-commit' hook failed with error output:
    The following files contain NOCOMMIT:
    trunk/workspace/main.cpp
     
    Please fix and attempt commit again.
     
    bash /tmp/xyz/workspace>

I propose you try and insert this in a comment in your source code any time you would otherwise make a mental note to get back to this place before commit. This has saved me from committing bad stuff countless times.

I have defined a keyboard shortcut in my editor to insert this string, so it is almost zero effort to insert it for me. Does anyone know to do this in eclipse?

I usually write a reason behind NOCOMMIT so I won't forget why I put it there. Common things I use it for:

    // NOCOMMIT comment this check|test|function back in before I commit 
    // NOCOMMIT temporary workaround
    // NOCOMMIT needs documentation
    // NOCOMMIT code is obsolete, delete when the new code works
    // NOCOMMIT implement properly
     
    printf("NOCOMMIT: some debug message");

How to install:

   cp nocommit.svn /path-to-svn-server-root/hooks/pre-commit

