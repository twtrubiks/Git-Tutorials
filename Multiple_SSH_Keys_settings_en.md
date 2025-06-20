# Multiple SSH Keys settings for different github account

[English Version](Multiple_SSH_Keys_settings_en.md)

If you are really unfamiliar with this, I suggest watching the video :smile:

* [Youtube Tutorial - Multiple SSH Keys settings for different github account](https://youtu.be/gDxG-4tF7B8)

## Foreword

Sometimes we may encounter a situation where we need to have multiple GitHub accounts on the same computer. Why?

When your work computer and your own side project development are on the same computer, you will need the help of this article :kissing_smiling_eyes:

Trust me, you don't want to use your company's account to push commits to your own side project :sweat_smile:

## Tutorial

First, generate an ssh key. If you don't know how to generate one,

you can refer to [Generating a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) or [Basic GitHub Tutorial - From Scratch](https://www.youtube.com/watch?v=py3n6gF5Y00).

Open your Git Bash.

```cmd
ssh-keygen -t rsa -b 4096 -C "blue555236sa56@gmail.com"
```

(Please replace the email with your own)

The key point here is to remember to enter a new rsa name yourself, like `/c/Users/twtrubiks/.ssh/id_rsa_rubik` in the picture below.

This way, you won't overwrite the old rsa.

![alt tag](https://i.imgur.com/2Msr51U.png)

Next, you will have a new file you just created in your `.ssh` path.

![alt tag](https://i.imgur.com/B4g9FQO.png)

Then paste your `id_rsa_rubik.pub` key to your GitHub.

![alt tag](https://i.imgur.com/tfQzFcJ.png)

Usually, when you add it successfully, you will receive an email.

Then enter the command below:

```cmd
ssh-agent -s
```

The above command must be executed. If you skip this step, the following error will occur:

`Could not open a connection to your authentication agent.`

So please remember to execute it.

Create a file named `config` in the `.ssh` directory (the file name is `config`, no extension is needed).

![alt tag](https://i.imgur.com/SJBxro6.png)

Below is an example:

```config
# github - twtrubiks
    Host github.com
    HostName github.com
    IdentityFile ~/.ssh/id_rsa
    IdentitiesOnly yes
    User twtrubiks

# github - blue-rubiks
    Host blue.github.com
    HostName github.com
    IdentityFile ~/.ssh/id_rsa_rubik
    IdentitiesOnly yes
    User blue-rubiks
```

You can use the following command to test. If your own username is displayed, it means the setting is successful.

```cmd
ssh -T git@github.com
```

![alt tag](https://i.imgur.com/rdLf4iX.png)

```cmd
ssh -T git@blue.github.com
```

![alt tag](https://i.imgur.com/YTNHPfN.png)

ya :heart_eyes: we have set it up successfully~

If there is a problem, you can also use debug mode to see where the problem is. Usually, it is an error in the `config` input.

```cmd
ssh -vT git@github.com
```

Next, let me explain to you first.

```cmd
git config --global user.name "blue-rubiks"
git config --global user.email "blue555236sa56@gmail.com"
```

`--global` means global. If it is not entered, it means that the repo under the directory will take effect.

Now let's clone a repo to play with (you can create one yourself).

```cmd
git clone git@github.com:blue-rubiks/github-ssh-test.git
```

Next, switch to the directory folder and enter the following command:

```cmd
git config user.name "blue-rubiks"
git config user.email "blue555236sa56@gmail.com"
```

Note that `--global` is not added here, so it only takes effect for the repo under that directory.

We find the `.git` folder in the repo, and then find the `config` file. The content is roughly as follows:

![alt tag](https://i.imgur.com/vT6GiYR.png)

The main thing is to modify line 9 to line 10, changing it to the `Host` you set.

Finally, you can commit and push with peace of mind.

If you really don't understand what I'm talking about, I suggest watching the video explanation. I will walk you through the operation :laughing:

## Execution Environment

* Win 10

## Reference

* [Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)

## Donation

The articles are all original after my own research and internalization. If it has helped you and you want to encourage me, you are welcome to buy me a cup of coffee :laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[Sponsor Payment](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
