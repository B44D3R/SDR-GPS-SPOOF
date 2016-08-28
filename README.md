# Getting Started with the HackRF One on Ubuntu 14.04


<h1>Hardware</h1>
<h3>SDR: HackRF One - 265€</h3>
https://greatscottgadgets.com/hackrf/ 
https://greatscottgadgets.com/ant500/

<h3>Clock: LeoBodnar Precision Frequency Reference GPS Clock - 197€</h3> http://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=234

<h3>Cables</h3>
Reduction SMA(M) - BNC(F) 50R
Coaxial cable BNC(M) - BNC(M) 1m 50R
USB A-B

<h2>Summary</h2>
https://mborgerson.com/getting-started-with-the-hackrf-one-on-ubuntu-14-04

<p>Figuring out what you need to install to get going can be a drag, so I&rsquo;ll spare you the work and tell you how to quickly get started on an Ubuntu 14.04 LTS system.</p>

<p>Don&rsquo;t worry, this is going to be relatively painless.</p>

<p>Here&rsquo;s what we&rsquo;re going to do:</p>

<ul>
<li>Install some dependencies,</li>
<li>Build and Install the <a href="https://github.com/mossmann/hackrf/tree/master/host">HackRF Host Software</a> (libraries and tools),</li>
<li>Install <a href="http://gnuradio.org/">GNU Radio</a>,</li>
<li>Build and Install <a href="http://sdr.osmocom.org/trac/wiki/GrOsmoSDR">GrOsmoSDR</a>,</li>
<li>Build and Install <a href="http://gqrx.dk/">Gqrx</a>, and finally</li>
<li>Use Gqrx to tune into a local FM radio station.</li>
</ul>

<h2>Install Dependencies</h2>

<ol>
<li><p>Install the build dependencies.</p>

<pre><code>$ sudo apt-get install git \
                       build-essential \
                       cmake \
                       libusb-1.0-0-dev \
                       liblog4cpp5-dev \
                       libboost-dev \
                       libboost-system-dev \
                       libboost-thread-dev \
                       libboost-program-options-dev \
                       swig
</code></pre></li>

<li><p>Create a working directory.</p>

<pre><code>$ mkdir ~/sdr
</code></pre></li>
</ol>

<h2>Build HackRF Host Software</h2>

<ol>
<li><p>Clone the HackRF repository.</p>

<pre><code>$ cd ~/sdr
$ git clone https://github.com/mossmann/hackrf.git
</code></pre></li>
</ol>

<p><strong>Note:</strong> When I cloned, I got changeset <code>740940f8</code>. As this article ages, you will likely get a different version, and that&rsquo;s okay. I&rsquo;m just recording this as a known-working version.</p>

<ol>
<li><p>Move to the hackrf/host directory.</p>

<pre><code>$ cd hackrf/host
</code></pre></li>

<li><p>Create the build directory, move to it, and use <a href="http://www.cmake.org/">Cmake</a> (installed earlier) to create the Makefiles required for building.</p>

<pre><code>$ mkdir build &amp;&amp; cd build
$ cmake ../ -DINSTALL_UDEV_RULES=ON
</code></pre></li>

<li><p>Build and Install.</p>

<pre><code>$ make
$ sudo make install
$ sudo ldconfig
</code></pre></li>
</ol>

<h2>Test the HackRF Device</h2>

<ol>
<li><p>Connect the your HackRF One.</p></li>

<li><p>Run the <code>hackrf_info</code> tool to get some device information.</p>

<pre><code>$ hackrf_info
Found HackRF board.
Board ID Number: 2 (HackRF One)
Firmware Version: ...
Part ID Number: ...
Serial Number: ...
</code></pre></li>
</ol>

<h2>Download and Install GNU Radio</h2>

<p>Now let&rsquo;s download and install GNU Radio.</p>

<pre><code>$ sudo apt-get install gnuradio \
                       gnuradio-dev \
                       gr-iqbal
</code></pre>

<p><strong>Note:</strong> When I installed, I got version 3.7.2.1.</p>

<h2>Download, Build, and Install GrOsmoSDR</h2>

<p>Now we&rsquo;ll download, build, and install <a href="http://sdr.osmocom.org/trac/wiki/GrOsmoSDR">GrOsmoSDR</a>. GrOsmoSDR is essentially middle-ware that allows GNU Radio to communicate with the HackRF software to control your HackRF One.</p>

<ol>
<li><p>Clone the GrOsmoSDR repository:</p>

<pre><code>$ cd ~/sdr
$ git clone git://git.osmocom.org/gr-osmosdr
</code></pre></li>
</ol>

<p><strong>Note:</strong> When I cloned, I got changeset <code>58d95b51</code>.</p>

<ol>
<li><p>Move to the repository:</p>

<pre><code>$ cd gr-osmosdr
</code></pre></li>

<li><p>Create the build directory, move to it, and use Cmake to create the Makefiles required for building.</p>

<pre><code>$ mkdir build &amp;&amp; cd build
$ cmake ../
</code></pre></li>

<li><p>Build and Install.</p>

<pre><code>$ make
$ sudo make install
$ sudo ldconfig
</code></pre></li>
</ol>

<h2>Download, Build, and Install Gqrx</h2>

<ol>
<li><p>Clone the Gqrx repository:</p>

<pre><code>$ cd ~/sdr
$ git clone https://github.com/csete/gqrx.git
</code></pre></li>
</ol>

<p><strong>Note:</strong> When I cloned, I got changeset <code>e9171ff9</code>.</p>

<ol>
<li><p>Move to the repository:</p>

<pre><code>$ cd gqrx
</code></pre></li>

<li><p>Create the build directory, move to it, and use <a href="http://qt-project.org/doc/qt-4.8/qmake-manual.html">qmake</a> (not Cmake) to create the Makefiles required for building.</p>

<pre><code>$ mkdir build &amp;&amp; cd build
$ qmake ../
</code></pre></li>
</ol>

<p><strong>Note:</strong> You may get a message about no prefix being given. This is ok.</p>

<ol>
<li><p>Build and Install.</p>

<pre><code>$ make
</code></pre></li>

<li><p>Run Gqrx</p>

<pre><code>$ ./gqrx
</code></pre></li>
</ol>

