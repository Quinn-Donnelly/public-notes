supports:: [[Github Actions]]

# Summary
A set of practices that will help mitigate the threat of script injection.
# Body
1. Don't trust the `github` context as the values in here can flow directly from the user. ei. branch names bad emails etc.
2. Make code run in [[Github Actions Action]] instead of script. If it is a simple script you want to run use a [[Javascript Action]] so that you can pass inputs as args instead of building the script with the input.
3. When using [[BASH]] as the script you can set the untrusted input as an environment variable so that it will be understood as a string and not interpreted when doing $ on it
4. When writing BASH use double quotes instead of single where possibele and follow - [[Bash Script Security Recommendations]]
5. 