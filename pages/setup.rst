===============
Setup
===============
To be able to develop programs in Java through Intellij, a few different programs are needed.

Download and Install Intellij
^^^^^^^^^^^^
#. Navigate to https://www.jetbrains.com/idea/download/ or google “install intellij” without quotes.
===============
#. Select your operating system.
#. Click the black download button below **Community** as we will not be using the paid **Ultimate** version
    
    .. image:: ../images/setup/eclipse/normal_1.png
    
#. After clicking the download button, a popup will appear asking where you would like to download the installer to on your computer.

#. Select the desktop and click Save.

    .. image:: ../images/setup/eclipse/normal_2.png

#. Once downloaded, double click the installer, which looks like this.

    `If you don't want Javadoc and source annotations, skip to 11.`
   
    .. image:: ../images/setup/eclipse/normal_3.png

#. After double clicking the icon you may be prompted to allow the Intellij Installer to make changes to your device. Clicking Yes is necessary for the installer to install the appropriate files to your computer’s hard drive.

    .. image:: ../images/setup/eclipse/normal_4.png

#. Click the next button to begin.

    .. image:: ../images/setup/intellij/installer1.png
    
#. Select a personalized download location, or simply click next to accept the default location.

    .. image:: ../images/setup/intellij/installer-installpath.png

#. Create a desktop shortcut or any file type associations, or simply click next to accept the default values.

    .. image:: ../images/setup/intellij/installer-shortcutsandassociations.png
    
#. Specific start menu folder, or accept the default value of “JetBrains” and click next.

    .. image:: ../images/setup/intellij/installer-startmenufolder.png
    
#. After clicking the install button IntelliJ will begin installing using the options you selected previously. You should see a screen that looks like this.

    .. image:: ../images/setup/intellij/installer-installbar.png
    
#. Click the checkbox beside Run IntelliJ IDEA Community Edition.

#. Now click Finish.

    .. image:: ../images/setup/intellij/installer-finish.png

You Are Done!

#. Double click on the ItelliJ icon to launch it.

#. Click 'Create New Project'

#. Click ‘Download JDK’

#. Read through the Oracle Binary Code License Agreement for Java SE and make a decision.

#. Click on the download for your corresponding operating system to download the JDK intaller.

#. Run the JDK installer and follow its installation insturctions.

#. Return to the intelliJ window and click the New box.

#. Locate your JDK installation, it should be location in C:/ProgramFiles/Java/JDK1.8

#. Check the ‘Create project from template’ box and select ‘Command Line App’

#. Click next and provide a name for your new project.

------------------

Gradle Setup
""""""""""""""""""

#. If you have *Eclipse IDE for Java Developers* installed, skip to **2.**, otherwise you need to install the *Buildship Gradle Integration plugin* first:
    -  Open up Eclipse and go to the Marketplace (located under the *Help* tab)
   
    -  Search for *'gradle'* and install **Buildship Gradle Integration** (`Plugin-Page <http://marketplace.eclipse.org/content/buildship-gradle-integration>`_)
   
    -  After the plugin is installed, relaunch Eclipse

#. Right click within *Package/Project Explorer* and select **New > Other...**
   
#. In the *Gradle* folder, select **Gradle Project**
   
#. Type a name for your Project and click on *Finish*. Your setup should look like this at this point:
   
#. Delete the classes within ``src/main/java`` and ``src/test/java``
   
#. Open up and edit the file ``build.gradle``
   
#. Replace its content with the following code:
    
    .. code-block:: groovy
        
        apply plugin: 'java'
        
        dependencies {
            compile 'net.dv8tion:JDA:X.X.X\_XXX'
        }
        
        repositories {
            jcenter()
        }
        
        task fatJar(type: Jar) {
            manifest {
                attributes 'Main-Class': 'your.main.class.goes.Here'
            }
            
            from { 
                configurations.compile.collect {
                    dependency ->
                    if (dependency.directory) {
                        return dependency
                    } else {
                        return zipTree(dependency)
                    }
                }
            }
            with jar
        }


    - Adjust the version of JDA you want to use (see dependencies-section of file) and fill in your Main-Class as soon as you have one (the one containing your `public static void main(String[] args)` method)

#. Save the file and do the following: *Right click your project > Gradle > Refresh All*

#. Once all of the dependencies have been downloaded, create your desired packages/classes in ``src/main/java`` and start coding!

------------------
