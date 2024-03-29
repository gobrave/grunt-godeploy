# grunt-godeploy
Grunt powered deployment

## Authentication
Before using godeploy, you have to install your public ssh key on the server. If you belong to the unfortunate ones(i.e. a disciple of Steve Jobs), you have to install ssh-copy-id: `brew install ssh-copy-id`. Run:

`ssh-copy-id user@123.123.123.123`



## Usage

 - Add the dependency to package.json:

    `"grunt-godeploy": "git+ssh://git@github.com/Useful-Innovation/grunt-godeploy"`

 - Load in Gruntfile:

    `grunt.loadNpmTasks('grunt-godeploy');`

 - Configure deploy targets as described below

 - Deploy by running `grunt godeploy` or build a new task that includes `godeploy`.
 - If you have multiple targets, run `grunt godeploy:production` to only deploy to a target named `production`


## Options
For all available options see [here](https://github.com/jedrichards/rsyncwrapper#options).

In addition, a `commands` option is available. See example below.

#### Default options

```javascript
{
    src:    './',   // Source is cwd
    args:   ['-a'], // Use archive mode
    delete: true    // Deletes objects in dest that aren't present in src. Ignores excludes.
}
```

## Config example
```javascript
{
    godeploy: {
        options: { // Options for all deploy targets
            src: './',
            commands: {
                remote: {
                    before: "",
                    after:  [
                        "mkdir -p animals",
                    ]
                },
                local: {
                    before: "",
                    after:  ""
                }
            },
            exclude: [
                "node_modules"
            ]
        },
        production: { // A deploy target
            options: { // target specific options
                exclude: ['node_modules','some_path/']
            }
            host:       "123.123.123.123",
            port:       "22",
            user:       "deploy",
            dest:       "/home/deploy/project"
        },
        staging: { // Another deploy target
            host:       "231.231.231.231",
            port:       "2200",
            user:       "deploy",
            dest:       "/home/deploy/project"
        }
    }
}
```

## Notes

### Commands
 - Commands can be strings or arrays of strings. Remote commands runs in provided destination and local commands runs in `./`.
