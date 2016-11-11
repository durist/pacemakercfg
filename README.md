# pacemakercfg
Perl script to manage pacemaker cluster configuration from a directory of XML files

This is useful for managing cluster configuration in small chunks of XML that can be templated, perhaps via a configuration management tool such as puppet. It has also continued to work robustly across many versions of pacemaker.

Requires XML::Twig module

Usage is thus:

    ./pacemakercfg [options...] xmldir
        
    Creates and installs a new CIB from the configuration defined by .xml
    files in the xmldir directory. Current configuration directives
    (resources, constraints and nodes) are deleted and replaced with the
    content from the .xml files.
        
    Runs crm_verify before installing new CIB; will not install CIB if 
    crm_verify reports any errors unless --no-verify option is given. This
    is required if any resources have been deleted.
        
    A backup of the CIB is created in the xmldir/backup directory.
    
    Must be root to use.
    
    Options:
      -h, --help        This message
      -n, --no-verify   Do not run crm_verify before installing new CIB;
                        required if you have deleted resources. Use with 
                        caution!
      -d, --dry-run     Dry run only; just runs crm_verify against merged XML
      -f, --file        Dump merged XML to file without updating CIB
      -b, --bump-epoch  Increment the admin_epoch attribute in the CIB 
                        (rarely needed)

