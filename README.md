# Xamarin notes

The canonical repository (`upstream`) for this fork is
https://android.googlesource.com/platform/external/sqlite/

The `main` branch here is kept in sync with the upstream `master` branch,
if you need to update you can do it by adding a remote and
merging its master branch into ours:

    $ git remote add upstream https://android.googlesource.com/platform/external/sqlite/
    $ git fetch upstream
    $ git merge upstream/master
    $ git push

We do not use the `main` branch for anything else than to keep it in sync with
Google upstream.  Whenever there's a need to update SQLite version a new branch
named after the SQLite version should be created off of the `main` branch and
the following procedure should be followed:

   * After the branch is created, download the amalgamation zip from https://sqlite.org/download.html
   * Copy the new amalgamation files to both the `dist` and `dist/orig` directories
   * Commit the changes
   * Apply `Android.patch` to the `dist` directory:

         $ cd dist
         $ patch -p0 < Android.patch
	
   * If there are hunks which failed to apply, fix them
   * Update `Android.patch`:
	
         $ git diff > Android.patch

   * Commit and push the above changes to GitHub

