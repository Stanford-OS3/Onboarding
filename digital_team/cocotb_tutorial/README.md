<h1> How to use CocoTB for design verification </h1>

<p> this page is currently being updated by Stan, and isn't finished yet. also, i am not the best web-developer so its not the best looking. sorry.... if you want to
help me make this better, you are welcome to! </p>

<h2>
  A Quick Introduction
</h2>
  <p> 
    Hi! This GitHub repository is made to help you verify your designs with a Python golden model and your RTL code. There may be a few bits to understand before tackling this though.
  </p>
    <h4>
      UNIX
    </h4>
      <p>
        If you aren't familiar with UNIX, it'd be helpful to get familiarized with it since knowing it is crucial to understanding how everything is installed and how to access
        certain files. You can reference <a href="https://linuxjourney.com/"> this link </a> to get familiarized with it, or you can take CS107, 
        which is a great introduction to computer systems!
      </p>
    <h4>
      other stuff to be added
    </h4>
  

<h2> 
  Installing Verilator
</h2>
  <p> 
    you don't have to use verilator, but if you are, there may be a few issues.
  </p>
  <h4>
    Apple Silicon Users
  </h4>
    <p>
      Unfortunately, we aren't able to find a way to get this working on Apple Silicon. If you were able to, please reach out and let us know! Good news is there is a way around this; we will
      use the myth machines (or any Stanford student accessible server you want to use)! Here is the process I used to get verilator working on the myth machines. Just for your own sake,
      it would make it easier to manage things if you kept files organized. You can use <a href="https://code.visualstudio.com/docs/remote/ssh"> this guide </a> to learn how to remote SSH
      into the server using VSC.
    </p>
    <h5>
      1. Run the following commands in the directory of your choice:
    </h5>
      <pre><code>
      git clone https://github.com/verilator/verilator
      cd verilator
      git checkout v5.022
      autoconf
      ./configure
      make
      </code></pre>
    <p>
      Now, you might notice (after waiting for the compiling process to finish) that there was a small error regarding help2man. The reason for this error is that we don't have this
      installed by default. Normally, you could install help2man easily, but because we don't have sudo access on the myth machines, we must use other methods!
    </p>
    <h5>
      2. Run the following commands in the directory of your choice:
    </h5>
      <pre><code>
      wget https://mirrors.ocf.berkeley.edu/gnu/help2man/help2man-1.49.3.tar.xz
      tar xvf help2man-1.49.3.tar.xz
      cd help2man-1.49.3/
      ./configure --prefix=$HOME/.local
      make
      make install
      </code></pre>
    <h5>
      3. Add the following lines to your .bashrc file:
    </h5>
      <pre><code>
      export PATH=$HOME/.local/bin:$PATH  
      export VERILATOR_ROOT="PATH TO YOUR VERILATOR DIRECTORY"
      export PATH=$PATH:"PATH TO YOUR VERILATOR BIN FILE (will just be the verilator root and just add /bin)"
      </code></pre>
    <p>
      Now you are almost done! Type <code> source ~/.bashrc </code> to get this working. 
    </p>
    <h5>
      4. Go back to the verilator directory and type "make" again!
    </h5>
    <p>
      After doing this, it should work. To make sure your verilator installed properly, type <code> verilator --version </code> and the 5.022 version should pop up.
    </p>
  <h4>
    For People who do not use Apple Silicon
  </h4>
    <p>
      Many of the steps required are very similar to what Apple Silicon users must go through since we installed verilator on an x86 server to get around this issue. If you
      are using your own machine, however, you will need to install some of the prerequisites (example: help2man). For a comprehensive 
      list, use <a href="https://verilator.org/guide/latest/install.html"> this link </a> to guide you.
    </p>
      
<h2>
  Installing CocoTB
</h2>
  <p>
    Run the following command: <br>
    <code> pip install cocotb </code> <br>
    This should work regardless of if you're working with your own device or using the myth machines.
  </p>

<h2>
  Using CocoTB
</h2>
  <p>
    Congrats! You have completed the installation process. Now, you will get to explore how it works. There are a few things to remember when using CocoTB. The important files are
    all of your HDL files and the python file running your Golden Model and tests. For reference, <a href="https://docs.cocotb.org/en/stable/"> ths link </a> contains documentation
    about CocoTB and should answer any questions you have.
  </p>
  <h4>
    Makefile
  </h4>
    <p>
      The Makefile allows you to specify your simulator (Verilator, Icarus-Verilog, etc) with SIM, the TOPLEVEL_LANG (Verilog in our case), our VERILOG_SOURCES (all the HDL files
      used in the design), our TOPLEVEL (top module that we will be testing that instantiates all the other modules - kind of like the wrapper for the entire design), and the MODULE 
      (testing file that will be used). Edit these to the settings of your environment/design.
    </p>
  <h4>
    Python Testing
  </h4>
    <p>
      In this repo, there is a basic file called <code> example_test.py </code>, which is just to get you familiarized with basic testing. If you look at the <code> ks_add_test.py </code> 
      file, you will see a complicated Python function, which is the Golden Model being used. You can see that each CocoTB test in the file will use this Golden Model. Anyways, if
      you have everything set correctly, you can type <code> make </code> in the directory containing all the HDL files, Python testing files, and the Makefile. The test should pass,
      and you have successfully used CocoTB to verify your design. Try doing this with the other modules in the repo and getting tests to pass. There should be no flaws in the designs.
    </p>

<h2>
  Conclusion
</h2>
  <p>
    With this short guide, you learned how to install Verilator and CocoTB, and you used them to test some pre-made designs and testing files. The guide was made to get you
    familiarized with CocoTB installation and the basics of using it. We encourage you to make your own designs and testing files, so you can get this working with designs
    we make in OS3. Again, if you want more information concerning syntax and other specific details, reference <a href="https://docs.cocotb.org/en/stable/"> this link </a>. 
    Thank you for Reading this guide, and feel free to provide any feedback!
  </p>

<h2>
  Credits
</h2>
  <p>
    This guide was written by Stan Lee, and all files were provided by Austin Brown for the Open-Source Silicon @ Stanford Club.
  </p>

  
