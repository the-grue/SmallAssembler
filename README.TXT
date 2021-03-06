                      Small Assembler User Notes
                            June 10, 1989


COPYRIGHT NOTICE
                      Copyright 1988 J. E. Hendrix
                          All rights reserved.


ASSEMBLER VERSION

This diskette contains version 1.2 (revision level 14) of Small Assembler.
Small Assembler is written in Small C primarily for use in processing
Small C compiler output; nevertheless, it is a surprisingly capable
assembler handling all of the 8086 family processors through the 80386
and their associated numeric processor extensions (NPXs).  At this stage
the Small Assembler runs quite slowly compared to Microsoft's latest
assembler.  But it is adequate for use with Small C, making it unnecessary
to purchase a more expensive companion assembler.

This assembler is essentially compatible with the Microsoft product.
Either may be used with the Small C assembler.  Differences are
primarily: (1) many Microsoft directives are not supported (most notably
the conditional assembly directives), (2) macros employ positional
rather than named parameters, (3) not all of the Microsoft expression
operators are supported, and (4) most of the expression operators in the
C language are supported.



THE DISTRIBUTION DISKETTE

The Small Assembler files have been compressed into two ZIP files as follows:

           file                       contains
        ----------      ---------------------------------------
        EXECUTE.ZIP     files needed to execute Small Assembler
        COMPILE.ZIP     files needed to compile Small Assembler

You must run PKUNZIP to unpack the ZIP files.  Follow these steps:

  1. Place the distribution diskette in drive A: (or B:)
     and make it the default drive.
  2. Enter:  A>PKUNZIP EXECUTE <destination>
  3. Enter:  A>PKUNZIP COMPILE <destination>

Examples:

  A>PKUNZIP EXECUTE C:\SA         unpack executable files to C:\SA

  A>PKUNZIP COMPILE C:\SA         unpack source files to B:



FILE LISTING

The following files are included on the distribution disk(s):

   READ.ME     This documentation.
   HISTORY     History of Small Assembler revisions.
   AR.C        Archive maintainer source.
   AR.EXE      Archive maintainer.
   ASM.EXE     Assembler.
   ASM.H       Assembler header file.
   ASM1.C      Assembler source, part 1.
   ASM2.C      Assembler source, part 2.
   ASM3.C      Assembler source, part 3.
   ASM4.C      Assembler source, part 4.
   ASM.ARC     Assembler library source archive.
   ASM.LIB     Assembler library.
   ASMARC.LST  Assembler library source archive list.
   ASMLIB.LST  Assembler library object module list.
   80X86.MIT   Machine Instruction Table for all CPUs.
   CMIT.C      Machine Instruction Table compiler source.
   CMIT.EXE    Machine Instruction Table compiler.
   DUMP.C      File dump utility source.
   DUMP.EXE    File dump utility.
   MIT.H       Header for Machine Instruction Table functions.
   NOTICE.H    Version and copyright header.
   OBJ1.H      Object file header, 1 of 3.
   OBJ2.H      Object file header, 2 of 3.
   OBJ3.H      Object file header, 3 of 3.
   STDIO.H     Standard Small C Header.
   ASMCAL.BAT  Compile & assemble one part of assembler, optionally link.
   CALIB.BAT   Compile, assemble, and place module in ASM.LIB.
   MANUAL.TXT  User's Manual


DOCUMENTATION

Since the manual is out of print it has been included on this diskette.
To print it, copy the file MANUAL.TXT to your printer.


USING THE ASSEMBLER

Small Assembler reads an ASCII source file and writes an object file
in the standard Microsoft OBJ file format.  This makes the Small Assembler
compatible with LINK which comes with most copies of DOS.  In fact, Small
Assembler has no linker of its own; so it must be used with the DOS linker.
I understand that IBM quit including LINK with its latest versions of PC-
DOS.  This could be a problem if you don't have ready access to copy of it.

The command line for invoking the assembler has the following format:

          ASM source [object] [-C] [-L] [-NM] [-P] [-S#]

Command-line arguments may be given in any order.  Switches may be
introduced by a hyphen or a slash.  The brackets indicate optional
arguments; do not enter the brackets themselves.

 source   Name of the source file to be assembled.  The default, and
          only acceptable, extension is ASM.  Drive and path may be
          specified.

 object   Name of the object file to be output.  It must have a OBJ
          extension to be recognized as the output file.  Drive and path
          may be specified.  If no object file is specified, output will
          go to a file bearing the same name and path as the source
          file, but with a OBJ extension.

 -C       Use case sensitivity.  Without this switch, all symbols are
          converted to upper-case.  With this switch, they are taken as
          is; upper- and lower-case variants of the same letter are
          considered to be different.  With or without this switch,
          segment, group, and class names are always converted to upper-
          case in the output OBJ file.

              Note: The .CASE directive may be included at the
              beginning of the source file to produce the same
              effect as this switch.

 -L       Generate an assembly listing on the standard output file.  If
          you do not want the listing to go to the screen, then provide
          a redirection specification (e.g., >prn or >abc.lst) to send
          it wherever you wish.

 -NM      No macro processing.  This speeds up the assembler somewhat.
          Macro processing is NOT needed for Small-C output files.

 -P       Pause on errors waiting for an ENTER keystroke.

 -S#      Set symbol table size to accept # symbols.  Default is 1000.

If an illegal switch is given, the assembler aborts with the message

        Usage: ASM source [object] [-C] [-L] [-NM] [-P] [-S#]

The null switch (- or /) can be used to force this message.

If the assembler aborts with an exit code of 1, there is insufficient
memory to run it.  Pressing control-S makes the assembler pause until
another key is pressed, and control-C aborts the run with an exit code
of 2.  If the program contained errors, an exit code of 10 is returned
and the output file is deleted. Press ENTER to resume execution after a
pause because of an error.



USING THE MIT COMPILER

CMIT.EXE compiles the source machine instruction table (80X86.MIT) to
obtain its object file (80X86.OBJ).  This program is invoked by the
command line:

           Usage: CMIT [-#] [-O] [-L] [table]

The switches can be introduced by hyphens or slashes.  The command line
arguments have the following values:

 -#     Highest numbered CPU to recognize:

            -0  =>  8086
            -1  => 80186
            -2  => 80286
            -3  => 80386

 -O     Output the indicated or default machine instruction table
        as an OBJ file.

 -L     List the compiled machine instruction table.

 table  Name of the Machine Instruction Table source file
        (default 80X86.MIT).  The default and only allowed
        extension is MIT.  A drive and path are allowed.

If no switches are given, -L is assumed.  If any switches are given, only
the actions specified are taken.

The object file created by CMIT must be linked into ASM.EXE.



USING THE ARCHIVE MAINTAINER

The archive maintainer AR.EXE collects text files into a single archive
file. Modules (files that exist within the archive) can be extracted, new
ones added, old ones replaced or deleted, and a list of the archive
contents produced. The command line for invoking AR.EXE is:

        AR switch archive [list]

 switch     The first argument is a required switch from the following set:

            -D  Delete listed modules from the archive.
            -P  Print listed, or all, modules on stdout.
            -T  Table of contents of listed or all modules to stdout.
            -U  Update the archive by adding/replacing modules from
                separate disk files (used to create a new library).
                If no file names are specified in the command line,
                they are obtained from stdin.
            -X  Extract listed, or all, modules into separate files.

 archive    The second argument is the name of the archive file. It must
            be complete with the filename extension.  Drive and path are
            optional.

 list       The third and subsequent arguments are module/file names.

Use control-S to pause execution and control-C to abort the run.

To extract all of the modules from the library archive enter:

                       AR -X ASM.ARC


SUGGESTIONS

Phase errors are caught only at labels. So to be absolutely sure one
doesn't slip by undetected, you should place a dummy label at the end of
the last instance of each segment.


HINTS FOR RECOMPILING THE ASSEMBLER

Any changes to ASM.H will usually require the recompiling of every
program source file that includes it.  That is ASM1.C, ASM2.C, ASM3.C,
ASM4.C, AND CMIT.C.  Before linking ASM, be sure to run CMIT to create a
new 80X86.OBJ containing the new #define constants.  Otherwise, things
won't match up properly.

In any case, you must run CMIT to generate 80X86.OBJ before your first
attempt to link the assembler.

See ASMCAL.BAT for the commands to perform the compiling, assembling, and
linking of the assembler.  Each run of ASMCAL.BAT compiles and assembles one
part of the assembler.  For example, to compile and assemble ASM1.C enter

                          ASMCAL ASM1

If all parts have not yet been compiled and asembled, or 80X86.OBJ has not
been created by running CMIT.EXE, then you can skip the link step at the end
by entering a control-C at the pause prompt. Pay careful attention to the
order of the library files in the link command.  Follow this order when
composing your own link commands.


MICROSOFT COMPATIBILITY

If the behavior of Small Assembler in automatically generating ASO and
OSO prefixes in 32-bit object files seems obscure and sometimes
inefficient, it is not without reason.  The actions taken are predicated
on compatibility with the Microsoft object file processing utilities that
will be coming down the pike in the future.  My assumption was that if
Microsoft did that way, they must have good reasons (well reasons
anyway).  Good or otherwise, any deviation is likely to create
incompatibilities with future Microsoft software.  In file ASM2.C the
symbol MASM_xOS is defined.  If this definition is deleted or commented
out, then ASM will generate more efficient 32-bit code.


                        James E. Hendrix
                        417 N. 11th Street
                        Oxford, MS  38655

