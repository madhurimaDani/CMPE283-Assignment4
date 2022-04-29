# CMPE283-Assignment4
## Assignment 4: Nested Paging vs. Shadow Paging

### Team Members
	•	Madhurima Subodh Dani (015261974)
	•	Shreemathi Duvvuri (015273102)

### [1] For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched.
- Madhurima
  - Executed steps required for assignment and collected snippets
  - Discussed on assignment questions and answers
- Shreemathi
  - Analyzed output and finalized answers for given questions
  - Created documentation and updated README.md

### [2] Steps Followed

- Followed up with Assignment 4 after completing steps for Assignment 3
- By default, with nested paging enabled, executed command file containing sequence of cpuid -l 0x4ffffffd -s xx commands
- From outer VM, checked messages by executing command: dmesg
#### With Nested Paging (With EPT)

<img width="414" alt="image" src="https://user-images.githubusercontent.com/51197183/165887394-02acf639-553a-45f5-86df-54a9bf60edae.png">

- From outer VM, checked messages by executing command: dmesg
- Enter into bash mode: sudo bash
- From outher VM, shut down the inner VM by executing command: sudo virsh shutdown madhurimaCentOS

<img width="491" alt="Screen Shot 2022-04-27 at 10 54 32 PM" src="https://user-images.githubusercontent.com/51197183/165884814-7b50e36f-4d54-4d21-97ff-920f170376f0.png">

- In outher VM, remove kvm_intel module by executing command: rmmod kvm-intel

<img width="419" alt="Screen Shot 2022-04-27 at 10 57 32 PM" src="https://user-images.githubusercontent.com/51197183/165884978-601960d4-2f04-46c3-8c21-9cb31340b5a3.png">

- In outher VM from linux dir, reload kvm_intel module with shadow paging by executing command: insmod /lib/modules/5.18.0-rc3+/kernel/arch/x86/kvm/kvm-intel.ko ept=0

<img width="485" alt="Screen Shot 2022-04-27 at 10 57 42 PM" src="https://user-images.githubusercontent.com/51197183/165885102-bacba051-cfd7-4cc1-ab17-7aff542e8da1.png">

- Start inner VM (which now has shadow paging enabled): sudo virsh start madhurimaCentOS

<img width="517" alt="Screen Shot 2022-04-27 at 10 58 27 PM" src="https://user-images.githubusercontent.com/51197183/165885223-226d300d-1374-49e2-9f8e-dfaa22dc9f9e.png">

- Open console for inner VM and log in: sudo virsh console madhurimaCentOS
- In inner VM, execute command file (./command.sh) and check messages in outer VM using dmesg
#### With Shadow Paging (Without EPT)

<img width="468" alt="image" src="https://user-images.githubusercontent.com/51197183/165887452-3a638bc6-471e-4be6-b63d-75c5fd44bc98.png">



### [3] Questions
- What did you learn from the count of exits? Was the count what you expected? If not, why not?
    - Exit count without EPT (shadow paging) is significantly higher as comapared to respective exit counts with EPT (nested paging). Shadow paging always causes more exits than nested paging, hence this behaviour was expected. This makes shadow paging slower.
    
- What changed between the two runs (ept vs no-ept)?
    - Exit count increased with no-ept for most of the non-zero exit counts from ept run.  Below table shows the exit count changes for ept vs no-ept run:
    
    <img width="366" alt="image" src="https://user-images.githubusercontent.com/51197183/165887622-7179bfba-495b-413e-8990-7a44b55bece6.png">
