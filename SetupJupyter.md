# Jupyter to run R

If `which R` and `.libPaths()` show correct outputs but the R kernel does not appear in JupyterLab, it likely means the IRkernel was not properly registered with Jupyter. Here's how to resolve the issue step-by-step:

---
### **Step 1: Verify Jupyter Installation**

Ensure that Jupyter is installed and accessible from your terminal:

```bash
jupyter --version
```

If this command fails, install Jupyter:

```bash
pip3 install --user jupyter
```

Add Jupyter to your `PATH` if needed:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

### **Step 2: Verify IRkernel Installation**

Open R and ensure that the IRkernel package is installed:

```R
installed.packages()["IRkernel", ]
```

If it's not installed, install it:

```R
install.packages("IRkernel")
```

---
### **Step 3: Register IRkernel with Jupyter**

Run the following command in R to register the kernel with Jupyter:

```R
IRkernel::installspec(user = TRUE)
```

- **If you want a system-wide installation** (requires admin privileges):

```R
IRkernel::installspec(user = FALSE)
```

This command tells Jupyter where to find the R kernel.

---

### **Step 4: Verify Kernel Registration**

Check if the R kernel is listed in Jupyter's available kernels:

```bash
jupyter kernelspec list
```

You should see an entry like this:

```
Available kernels:
  python3      /path/to/python3/kernel
  ir           /home/username/.local/share/jupyter/kernels/ir
```

If `ir` (the R kernel) is not listed, manually install it using the path provided by `IRkernel::installspec()`:

1. Find the path to the IRkernel's `kernelspec` directory:

```R
system.file("kernelspec", package = "IRkernel")
```

2. Manually install the kernel:

```bash
jupyter kernelspec install /path/to/kernelspec --user --name=ir
```

---
### **Step 5: Restart JupyterLab**

Restart your JupyterLab server to refresh the kernel list:

```bash
jupyter lab
```

Check if "R" appears as an option in the kernel dropdown menu.

---

### **Step 6: Troubleshooting**

#### **Issue: Multiple Jupyter Installations**

If you have multiple Jupyter installations, ensure you're using the correct one. Use `which jupyter` to confirm its location.

#### **Issue: Missing Dependencies**

Ensure required system libraries are installed (e.g., `libzmq3-dev` for ZeroMQ):

```bash
sudo apt-get install libzmq3-dev
```

#### **Issue: Incorrect PATH**

Ensure that both `jupyter` and `R` are in your `PATH`. For example:

```bash
export PATH="/usr/local/bin:$HOME/.local/bin:$PATH"
```

#### **Issue: Kernel Still Missing**

Reinstall IRkernel and re-register it:

1. Remove existing IRkernel:

```R
remove.packages("IRkernel")
```

2. Reinstall and register:

```R
install.packages("IRkernel")
IRkernel::installspec(user = TRUE)
```

---

By following these steps, you should be able to see and use the R kernel in JupyterLab. If problems persist, ensure that your R installation and Jupyter are properly configured and compatible.

Reference

[^1]: https://stackoverflow.com/questions/44056164/jupyter-client-has-to-be-installed-but-jupyter-kernelspec-version-exited-wit
[^2]: https://github.com/IRkernel/IRkernel
[^3]: https://community.anaconda.cloud/t/r-kernel-error-in-jupyter-notebook/5500
[^4]: http://richpauloo.github.io/2018-05-16-Installing-the-R-kernel-in-Jupyter-Lab/
[^5]: https://cran.r-project.org/web/packages/IRkernel/readme/README.html
[^6]: https://docs.ncsa.illinois.edu/systems/delta/en/latest/user_guide/ood/custom-r.html
[^7]: https://discourse.jupyter.org/t/jupyter-notebook-kernel-issue/17954
[^8]: https://github.com/IRkernel/IRkernel/issues/595
[^9]: http://richpauloo.github.io/2018-05-16-Installing-the-R-kernel-in-Jupyter-Lab/
[^10]: https://yd-dev.tistory.com/12
[^11]: https://github.com/IRkernel/IRkernel/issues/583
[^12]: https://bioinfoblog.tistory.com/94
[^13]: https://www.nas.nasa.gov/hecc/support/kb/how-to-set-up-r-kernel-in-jupyter-lab_685.html
[^14]: https://stackoverflow.com/questions/56454835/will-installing-irkernel-via-cran-work-in-my-conda-environment
[^15]: https://github.com/IRkernel/IRkernel/issues/595
[^16]: https://discourse.jupyter.org/t/jupyterhub-irkernel-misbehaving-next-steps-for-debugging/12160
[^17]: https://irkernel.github.io/installation/
[^18]: https://www.linkedin.com/pulse/installing-r-kernel-jupyter-lab-david-effendi
[^19]: https://discourse.jupyter.org/t/problems-running-rstudio-on-jupyterhub/13211
[^20]: https://discourse.jupyter.org/t/r-kernel-wont-start/13713
[^21]: https://discourse.jupyter.org/t/missing-icons-at-top-of-notebook/21666
[^22]: https://stackoverflow.com/questions/67107296/r-kernel-in-jupyterlab-does-not-display-axis-properly
[^23]: https://jupyter-notebook.readthedocs.io/en/stable/troubleshooting.html
[^24]: https://github.com/ContinuumIO/anaconda-issues/issues/8419
[^25]: https://github.com/jupyterlab/jupyterlab/issues/17211
[^26]: https://github.com/jupyterlab/jupyterlab/issues/6633
[^27]: https://www.reddit.com/r/Jupyter/comments/1e9cb7x/jupyter_lab_cell_glitch/
[^28]: https://github.com/IRkernel/IRkernel/issues/738
[^29]: https://blog.naver.com/kisudsoe/221203356429
[^30]: https://developers.lseg.com/en/article-catalog/article/setup-jupyter-notebook-r
[^31]: https://stackoverflow.com/questions/79132626/jupyter-lab-interface-icons-are-missing-how-to-fix
[^32]: https://superuser.com/questions/1479040/r-syntax-highlighting-in-jupyter-lab-not-working
[^33]: https://www.youtube.com/watch?v=G0twUZGSL_0
