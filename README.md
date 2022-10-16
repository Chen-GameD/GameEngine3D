# GameEngine3D - Mingyuan Chen
This is the assignment content of the course EAE6320, a project created based on Professor Tony's basic 3D engine template. My main work is to optimize the engine file based on the template, provide a good interface for users to use, and at the same time need to consider the compatibility of OpenGl and D3D graphics libraries and X86 and X64 platforms. And design a new system (animation system, collision system, audio system, etc.) at the end of the course to complete this course.


## Getting started

Clone this project, then open ChenMingyuan.sln. Build the project to ensure that both x86 and x64 can be successfully built.
Looking at the Solution Explorer window, there are five folders for the solution:  
1. Engine: It contains multiple projects, and references and dependencies have been set between projects.  
2. ExampleGame: The template's game layer project folder can be ignored and used to create my own MyGame folder.  
3. External: The engine will use Lua as the configuration file, and parsing scheme of Mesh and Shader, so External contains the Lua library; there are also Mcpp and OpenGlExtensions.  
4. MyGame: The project folder I created to serve the game layer, which contains the BuildMyGameAssets and MyGame projects.  
5. Tools: It is used for projects of configuration files such as BuildMesh and Shader. Its functions are mainly to process some data and copy files (copy to the output folder after Build, which is used for game data).  

## Description
This project can perform some basic operations of the game engine:  
1. You can create your Mesh file and then provide it to the engine for rendering at the game layer (the file storage path is: ```MyGame_/Content/Meshes```). Before submitting, you need to update the AssetsToBuild.lua file and add the path for the new file;  
2. You can create your Shader file and then submit the game layer to the engine for binding (the file storage path is: ```MyGame_/Content/Shaders```). Before submitting, you need to update the AssetsToBuild.lua file and add the path for the new file;  
3. The engine provides an interface to submit these new files to the engine and perform rendering:  
```
eae6320::Graphics::cEffect::CreateEffect(cEffect*& o_effect, const char* i_vertexShaderAddress, const char* i_fragmentShaderAddress);  
eae6320::Graphics::cMesh::CreateMeshWithLuaFile(cMesh*& o_mesh, const char* const i_path);  
```
4. The engine provides an interface to change the camera position and background color:  
```
eae6320::Graphics::SubmitCamera(Camera& i_camera, const float i_elapsedSecondCount_sinceLastSimulationUpdate);  
eae6320::Graphics::SubmitBackBufferColor(const float r, const float g, const float b, const float a);  
```
5. Add the content of the key input to ```eae6320::cMyGame::UpdateSimulationBasedOnInput()``` to update the game operation logic;  
6. Add the logic of game physics update to ```eae6320::cMyGame::UpdateSimulationBasedOnTime(const float i_elapsedSecondCount_sinceLastUpdate)``` for automatic physics update;  
7. Note:  
```
struct GameObjectData  
{  
    eae6320::Graphics::cMesh* m_Mesh = nullptr;  
    eae6320::Graphics::cEffect* m_Effect = nullptr;  
    //rigidbody  
    eae6320::Physics::sRigidBodyState m_RigidBodyState;  
};  
```
It is a structure I temporarily created to store Game Object data, which contains mesh information, shader information, and physical information;  
8. Note:  
```
struct Camera  
{  
    Physics::sRigidBodyState m_RigidBodyState;  
    float m_verticalFieldOfView_inRadians = Math::ConvertDegreesToRadians(45);  
    float m_aspectRatio = 1.0f;  
    float m_z_nearPlane = 0.1f;  
    float m_z_farPlane = 100;  
};  
```
It is a structure I use to store camera information; changing this data and submitting it to the engine using the interface can change the camera's position, depth, rotation, etc.  

## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation
Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage
Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support
Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.

## Integrate with your tools

- [ ] [Set up project integrations](https://eae-git.eng.utah.edu/eae6320-fall2022/chenmingyan/-/settings/integrations)

## Collaborate with your team

- [ ] [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
- [ ] [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
- [ ] [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
- [ ] [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
- [ ] [Automatically merge when pipeline succeeds](https://docs.gitlab.com/ee/user/project/merge_requests/merge_when_pipeline_succeeds.html)

## Test and Deploy

Use the built-in continuous integration in GitLab.

- [ ] [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/index.html)
- [ ] [Analyze your code for known vulnerabilities with Static Application Security Testing(SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
- [ ] [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
- [ ] [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
- [ ] [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)
