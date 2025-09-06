# Practical Task 1. Installing the Environment, Creating, and Running a Control Expert Classic Project

**Duration**: 2 hours

**Objective:** Learn how to install and launch Control Expert Classic and the PLC simulator.

## Laboratory Setup

**Required Hardware.** For performing the laboratory tasks, you need a computer with the following minimum hardware configuration:

- Intel/AMD CPU 2 GHz / RAM 16 GB / Disk 20 GB (free space)

**Required Software.**

1. Control Expert V16.2 distribution package
2. It is assumed that a virtual machine with VirtualBox will be used (https://www.virtualbox.org).
3. Internet browser and Internet access.

**General task statement.**

Work objectives:

1. Prepare a virtual workstation for conducting various laboratory tasks using Control Expert.
2. Create a new project in Control Expert Classic for a PAC M580 with a minimal configuration.
3. Compile the project and download it into the PLC Simulator.

## Work Procedure

### 1. Installing the VirtualBox Virtual Machine and Checking Virtualization

**This step is not mandatory if you plan to install Control Expert V16.2 on the native host OS, or if you already have a modern Windows OS installed.**

- [ ] Install VirtualBox and a virtual machine with Windows 10 OS as described at [this link](https://asu-in-ua.github.io/atpv/vm/vbox/labwin10.html).

### 2. Installing Control Expert

You can watch a video recording of the installation on YouTube [at this link](https://youtu.be/bHdi-KfJgqk).

- [ ] Download the EcoStruxure Control Expert image. At the time of writing this practical task, it can be downloaded from the following links:
  - [From the SE website, requires free registration](https://www.se.com/au/en/download/document/EcoStruxureControlExpert_V162/)
- [ ] Open the image or mount it into the virtual drive of the virtual machine.
- [ ] Install Microsoft .NET 3.5 if it is not already installed; it can be downloaded from the [Microsoft website](https://www.microsoft.com/en-us/download/details.aspx?id=21).
- [ ] Install EcoStruxure Control Expert, keeping all settings as default.

### 3. Creating a Project with M580 in Control Expert Classic

A video recording of creating a project with M580 and its first launch in the simulator can be viewed on the YouTube channel [at this link](https://youtu.be/xh5O392nYJ0).

**This procedure includes simple steps for quickly creating and running a project and involves disabling certain options that affect cybersecurity. In this example, it is done intentionally to simplify the practical task.**

- [ ] Launch Control Expert Classic (not Control Expert!).
- [ ] If you do not have a license, you can run the environment in Trial mode, i.e., activate a Trial license for 30 days. This should be sufficient to get familiar with the environment. To activate a Trial launch without running the License Manager, in the dialog window (Fig. 1.1) select `No`.

![image-20250906121009083](media/image-20250906121009083.png)

Fig. 1.1. Trial license warning window.

- [ ] Create a new project using the menu `File->New`.

  A PLC selection window will appear (Fig. 1.2). In this window, you can choose the PLC model and chassis configuration (these settings can also be changed later). If you need to specify a PLC with another (older) operating system version, you must activate the option `Show all versions`.

- [ ] In the PLC selection window, select `Modicon M580 BME P58 3040` with the latest version available (in Fig. 1.2 it is 4.40).

![image-20250906121143704](media/image-20250906121143704.png)

Fig. 1.2. PLC selection window.

- [ ] In the window that appears (Fig. 1.3), you will be asked to enter an application password that allows protecting parts of the project from read or write access. In this task, select the option to refuse the password `I don't want ...` and press `Ok`.

![image-20250906121230945](media/image-20250906121230945.png)

Fig. 1.3. Password creation window.

- [ ] Look at the project contents using the structured view in the `Project Browser` window (Fig. 1.4). Try to understand the purpose of each project section.

![image-20250906124059975](media/image-20250906124059975.png)

Fig. 1.4. Project Browser.

### 4. Changing Security Settings

**This procedure disables all possible security functions. In this example, it is done intentionally to simplify the practical task.**

- [ ] In the `Project Browser`, under the `Configuration` section, click the `EIO` icon (Fig. 1.5).

![image-20250906124922779](media/image-20250906124922779.png)

Fig. 1.5. Selecting network configuration.

The configuration window for the embedded communication channels of the M580 CPU will open (Fig. 1.6). It contains many tabs where the communication properties are configured depending on their activation. By default, almost all communication services are deactivated. This follows the security policy where everything is forbidden by default, and only the services required by the project are enabled afterward. For quick activation of all services (everything allowed), on the `Security` tab you can press the `Unlock Security` button. For deactivation (maximum protection), press `Enforce Security`. **Note that if you leave maximum protection (default) without additional changes to the settings, then when the project is downloaded to the M580, communications will only be available through the USB port, since all other communication services will be deactivated.**

- [ ] Review the contents of all tabs in the `EIO` configuration window, then return to the `Security` tab.

![image-20250906121356713](media/image-20250906121356713.png)

Fig. 1.6. Configuration window of the embedded communication channels of the M580 CPU with services deactivated (default).

- [ ] In the `EIO` configuration window, press the `Unlock Security` button. Disable the following services: `SNMP` and `HTTPS`. The contents of the tab will look like Fig. 1.7.

![image-20250906121446259](media/image-20250906121446259.png)

Fig. 1.7. `Security` settings for the practical task.

- [ ] To validate (apply to the project) the settings, select `Edit -> Validate` in the menu.
- [ ] Analyze the project for errors using `Build -> Analyze Project`.

Errors will be displayed in the corresponding tab (Fig. 1.8). At this stage, there should be errors related to the requirement to set passwords for firmware download (`Firmware`) and for securing the data storage (`Data Storage`). `Control Expert` allows you to navigate to the location of the error in the project by clicking the corresponding message.

![image-20250906121547464](media/image-20250906121547464.png)

Fig. 1.8. Window with errors after project analysis.

- [ ] Click the error message in the error window. The project properties window will open (Fig. 1.9) on the `Project & Controller Protection` tab.

For reference: the project properties window can also be opened via the context menu (Fig. 1.10).

![image-20250906114534616](media/image-20250906114534616.png)

Fig. 1.9. Project properties window.

![image-20250906114504794](media/image-20250906114504794.png)

Fig. 1.10. Accessing the project properties window via the project context menu.

- [ ] Click the `Change Password` button in the `Firmware` section (see Fig. 1.9). In the `Old password` field, enter the default password specified in the same window. In the `New Password` fields, enter a new password with at least 8 characters, including at least one uppercase letter, one lowercase letter, one number, and one special character.

![image-20250906114640688](media/image-20250906114640688.png)

Fig. 1.11. Changing the `Firmware` password.

- [ ] Similarly, change the password for `Web Diagnostic/Data Storage` (Fig. 1.12).

![image-20250906114704339](media/image-20250906114704339.png)

Fig. 1.12. Changing the password for `Web Diagnostic/Data Storage`.

- [ ] Analyze the project again for errors using `Build -> Analyze Project`. This time, the error list should be empty.

### 5. Creating a Section

- [ ] From the `Project Browser`, open the context menu of `Logic` and create a new program section (Fig. 1.13).

![image-20250906114802630](media/image-20250906114802630.png)

Fig. 1.13. Creating a new section.

- [ ] In the `Name` field, enter the section name (Fig. 1.14). You can change it later if needed. In the `Language` field, select the section programming language `LD`. This property cannot be changed after the section is created. Then click `Ok`.

![image-20250906114947465](media/image-20250906114947465.png)

Fig. 1.14. Section properties.

- [ ] The `LD` graphical editor will open, where you need to create the user program shown in Fig. 1.18. Place contacts and coils by selecting them from the menu (Fig. 1.15) or from the quick access toolbar (Fig. 1.16).

![image-20250906120349355](media/image-20250906120349355.png)

Fig. 1.15. Object palette via the menu.

![image-20250906120416954](media/image-20250906120416954.png)

Fig. 1.16. Object palette via the quick access toolbar.

- [ ] For the contact and coil, assign variables named `bool1` and `bool2`, respectively. If you specify a name of a non-existent variable, the editor will suggest creating it (Fig. 1.17). Click the check mark to accept the suggestion.

![image-20250906120315698](media/image-20250906120315698.png)

Fig. 1.17. Dialog suggesting variable creation.

![image-20250906114852958](media/image-20250906114852958.png)

Fig. 1.18. User program view.

- [ ] Check the created variables by clicking `Elementary variables` in the `Project Browser`.

![image-20250906120533901](media/image-20250906120533901.png)

Fig. 1.19. Variable list in the `Variables` window.

- [ ] Check whether there are any errors in the project by invoking the menu command `PLC -> Analyze`. If there are no errors, proceed to the next step. If there are errors, carefully verify that all actions were performed correctly.

### 6. Compiling and Running the PLC Simulator

To download the project into a PLC, it must first be compiled (`Build`). In this task, instead of a real controller, the PLC Simulator is used. It allows you to test the execution logic of the user program, but it has certain limitations and differences compared to a real PLC. A compiled project for the Simulator differs from a compiled project for a real PLC.

- [ ] Select the compile and connection mode (Fig. 1.19) as `Simulation Mode`.

![image-20250906115102862](media/image-20250906115102862.png)

Fig. 1.19. Selecting compile and connection mode.

- [ ] Compile the project (Fig. 1.20) using `Rebuild All Project`.

The first time, a full compilation is performed. After making changes in the project, you can also use partial compilation of changes (`Build Changes`). This allows you, in online mode with a PLC or Simulator, to apply changes during compilation without fully downloading the project and stopping the PLC.

![image-20250906115144594](media/image-20250906115144594.png)

Fig. 1.20. Menu commands for project compilation.

- [ ] In the error window, verify that there are no `Rebuild` errors.
- [ ] Use the menu command `PLC -> Connect` to connect to the Simulator (Fig. 1.21).

![image-20250906115255879](media/image-20250906115255879.png)

Fig. 1.21. PLC connection command.

- [ ] Since the PLC Simulator has not been started yet, the first launch will display a warning regarding access restrictions to the PLC Simulator (Fig. 1.22). The warning explains access protection options for the PLC Simulator through port 502: either via password or without restrictions. Click `Ok`.

![image-20250906115335618](media/image-20250906115335618.png)

Fig. 1.22. Warning window regarding PLC Simulator access restriction.

- [ ] In this example, we will not apply access restrictions to the PLC Simulator. Therefore, in the next Options panel window (Fig. 1.23), deactivate the option `Use default application to start simulator (enforce security)`. Click `Ok`.

![image-20250906115431690](media/image-20250906115431690.png)

Fig. 1.23. PLC Simulator Options panel.

After this, the PLC Simulator will start, and its indicator will appear in the Tray (Fig. 1.24). The `?` status indicates that no program is present in the PLC Simulator, which corresponds to `NO CONF` on the Control Expert Classic status bar (Fig. 1.25).

![image-20250906115715207](media/image-20250906115715207.png)

Fig. 1.24. Tray indicator after starting the PLC Simulator.

- [ ] Press `PLC -> Connect` again. Check the indicators on the status bar (Fig. 1.25):
- [ ] The `HMI R/W mode` indicator shows that online mode allows project modifications in the PLC.
- [ ] The `Different` indicator on the status bar shows that the compiled projects differ between the PLC Simulator (empty) and Control Expert (compiled version).
- [ ] The `NO CONF` indicator shows that the PLC Simulator has no project loaded.
- [ ] The `NO UPLOAD INFO` indicator shows that there is nothing to upload (source code) from the PLC Simulator.
- [ ] The `TCPIP:127.0.0.1` indicator shows the IP address of the PLC Simulator, and the yellow color reminds us that this is not a real PLC but a Simulator.

![image-20250906144249758](media/image-20250906144249758.png)

Fig. 1.25. Status bar in online mode without a project loaded in the PLC.

- [ ] Use the menu command `PLC -> Transfer Project to PLC` (Fig. 1.26).

![image-20250906115558784](media/image-20250906115558784.png)

Fig. 1.26. Command to transfer the project to the PLC.

- [ ] A window will appear showing which project is in Control Expert (PC) and which is currently in the PLC (Fig. 1.27). Select the `PLC Run after Transfer` option to ensure the program starts in the PLC after the full download.

![image-20250906115811510](media/image-20250906115811510.png)

Fig. 1.27. Project transfer window.

- [ ] After the transfer, a confirmation window will appear to start the program in the PLC (Fig. 1.28). Click `Ok`.

![image-20250906115836651](media/image-20250906115836651.png)

Fig. 1.28. Confirmation window to start the program.

- [ ] After starting the program, use the PLC Simulator context menu (Fig. 1.29) to open the `Simulation Panel...`.

![image-20250906115905695](media/image-20250906115905695.png)

Fig. 1.29. PLC Simulator context menu.

- [ ] Observe the appearance of the Simulation Panel (Fig. 1.30). Identify the indicator that, in your opinion, shows the state of the user program in the PLC.

![image-20250906115935067](media/image-20250906115935067.png)

Fig. 1.30. PLC Simulator panel.

- [ ] Look at the status bar. Compare the status values with Fig. 1.25. Try to determine the meaning of each indicator on your own.

![image-20250906153446114](media/image-20250906153446114.png)

Fig. 1.31. Status bar in online mode after the project is loaded.

### 7. Program Operation Check

In online mode, the section editor by default displays the status of variables and graphical elements. This display mode is called `Animation` and can be deactivated if necessary via the corresponding menu command or quick access toolbar (Fig. 1.32).

![image-20250906120013222](media/image-20250906120013222.png)

Fig. 1.32. LD program editor in online mode with the `Animation` option enabled.

In this case, for the LD language, green color of an element or connection indicates “voltage present” on it, while red indicates its absence. For Boolean variables, green corresponds to the value `TRUE`, while red indicates the state `FALSE`. As shown in Fig. 1.32, the contact does not “pass conditional current further” because the variable assigned to it (`bool1`) has the logical value zero (`FALSE`). Therefore, there is no “potential difference” at the coil, it does not activate, and consequently `bool2` remains `FALSE`.

The editor in online mode also has built-in debugging tools that allow changing variable values, although standard instruments such as the `Animation Table` and `Operator Screen` are also available for this purpose.

- [ ] Using the contact’s context menu, change the value of the variable bound to it (`bool1`) to `TRUE` (`Set to 1`).

![image-20250906120700624](media/image-20250906120700624.png)

Fig. 1.33. Changing variable values through the editor’s context menu.

- [ ] Observe the animation status of the LD editor elements. Think about why they are displayed in this way.
- [ ] Using the menu command `File -> Save as...`, save the project to disk and close the Control Expert Classic editor.