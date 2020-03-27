# Perlbrew
Perlbrew is a tool to manage multiple perl installations. Allowing for testing your production code against different perl versions, while leaving the vendor perl alone. You can even run your programs against all installations of perl. 

## Perl
Install a specific perl version.
```Bash
$ perlbrew install perl-5.26.0
```

Use a specific perl version in your current shell, run:
```Bash
$ perlbrew use perl-5.26.1
``` 

> We are disallowing the use of `perlbrew switch` completely. This will change the environment for all people on the machine and now just for your own user!

## Cpanm
Is a lightweigth CPAN client, which facilitates installing CPAN perl modules. It is a good idea to install it together with Perlbrew to always make them available across each your perlbrew perl installations i.e the CPANM library will change with the perlbrew switch command. 
Installing CPANM with perlbrew is done by this command:
```Bash
$ perlbrew install-cpanm
``` 
Perlbrew makes it easy to create and switch between multiple libraries of CPAN modules. You can even have several libraries for the same distribution of perl.
Here are some examples:
``` Bash
## To create a library named Basil to perl version 5.26.0 
$ perlbrew lib create perl-5.26.0@Basil

## To switch library for that perl distribution permanently
$ perlbrew switch perl-5.26.0@Basil

## If you have another library that you want to use for your current session 
$ perlbrew use perl-5.26.0@Manuel

## To delete your Manuel library 
$ perlbrew lib delete perl-5.26.0@Manuel

## You can view your perl distributions and libraries by running:  
$ perlbrew list  
```
If you need to reinstall a specific version of a cpanm library, run:
```Bash
$ cpanm --reinstall [your_cpanm_lib]@[version]
```

More information on perlbrew is available on [metacpan].

[Perlbrew]: https://perlbrew.pl
[metacpan]: https://metacpan.org/pod/distribution/App-perlbrew/bin/perlbrew
