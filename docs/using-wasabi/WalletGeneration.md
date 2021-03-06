---
{
  "title": "Wallet Generation",
  "description": "A detailed guide about the wallet and the key generation in Wasabi. This is the Wasabi documentation, an archive of knowledge about the open-source, non-custodial and privacy-focused Bitcoin wallet for desktop."
}
---

# Wallet Generation

With Wasabi you can generate an unlimited number of Bitcoin wallets very fast, without any cost, and without asking anyone for permission.
Each wallet has separate private and public keys in a unique backup, and they are not at all linked to the other wallets generated on the same computer.
So, with several wallets you can conveniently manage your bitcoin for different use cases without worrying about revealing that you control them.

[[toc]]

---

## Generating the wallet step-by-step

1. Launch Wasabi Wallet.
The very first time you run the software the `Generate Wallet` tab will automatically be open, but you can also access it by clicking on `File -> Generate Wallet` in the menu bar.

2. Label the new wallet precisely to ensure a proper differentiation at any point in the future.
This label is not shared with anyone, it is only stored locally on your computer.

3. Write a long and random password and _back it up_.
It encrypts your secrets and you will need it every time you want to spend bitcoin from this wallet, or recover your wallet.

Consider using [diceware wordlists](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases) or a secure password generator to protect yourself against brute force attacks.

:::danger Backup your password!
Without the password, you cannot spend your bitcoin or recover your wallet, even if you have the recovery words (Seed phrase).
So, triple-check that you have a proper backup!
:::

4. Click the checkbox after carefully reading the Terms and Conditions, the Privacy Policy and the Legal Issues of zkSNACKs Ltd. and Wasabi Wallet.

5. Click the `Generate` button.

![](/WalletManagerGenerateWallet.png)

6. Write down the 12 recovery words (Seed phrase).
You can use this seed phrase _with_ your password to recover your wallet on a different computer using Wasabi or another [BIP 38](/using-wasabi/BIPs.md#bip-38-password-protected-private-key) compliant wallet.
If you have only the recovery words, but not the password, then you cannot spend the bitcoin nor recover this wallet.
But whoever has both, gets full access to all the transaction history and gains control over every satoshi locked up in this wallet.

:::danger Backup your recovery words!
Without the recovery words (Seed phrase) AND the password, you cannot recover your wallet.
So, triple-check that you have a proper backup!
Make sure the backup of your recovery words is stored separately from the password backup.
:::

![](/WalletManagerRecoveryWords.png)

7. Test the password before you can load the wallet, to make sure that your backup password is correct.
So, type or paste the password in the text box, and click `Load Wallet`.

![](/TestPassword.png)

## What password to choose

Wasabi integrates [BIP 38: Password-Protected Private Key](/using-wasabi/BIPs.md#bip-38-password-protected-private-key), which means that the secrets needed to spend the bitcoin are encrypted on the computer.
If someone has compromised your operating system and hardware and he only has the encrypted secrets, then no bitcoin can be spent by him.
You need **both** the encrypted secrets, and the password in order to enable the private key which can sign a spending transaction.
This means that the password is your last line of defense against anyone who tries to steal your bitcoin.

:::tip
It is strongly recommended to use long and random passwords for everything, especially for your money!.
:::

### What not to do

Here are a couple of examples that do it completely wrong. 
You should not generate your password like this:

1. Do not use publicly known information like your grandma's maiden name and the birthday of your dog.
`Emma1992` is a really, really, really bad password, because it can easily be guessed and it is very short.

2. Do not use the same password that you have used in other places.
Because if one password is leaked, then other ones are compromised.

3. Do try to use a mix of uppercase and lowercase letters, numbers, and special characters (&$%@ etc.) in your password.

### Best Practices

Don't roll your own crypto.
You shouldn't try to re-invent the wheel for something as complicated and nuanced as cryptography, and especially in regards to entropy.
These are some of the industry best practices:

1. Rolling a dice might be the easiest way to get high entropy and randomness in numbers.
You can also use the [Diceware tutorial](/using-wasabi/WalletGeneration.md#create-strong-passwords-with-diceware) to get something similar to your Bitcoin recovery words (Seed phrase).
Now you have a verbal password that was generated completely off-line with sufficient randomness.

2. Flip through the pages of a book, stopping on an arbitrary page and pick up one word somewhere on that page.
Although this is not as random as a dice-roll, there is still a large set of possible words in a book.
You can further increase the randomness by selecting different books.

3. Use a well tested password manager with a cryptographically secure random number generator.
A good password manager will use sufficient entropy to generate a password with letters, numbers and special characters.
Although this is on-line and digital, a good password manager should still be secure enough for most cases.

## Create Strong Passwords with Diceware

Diceware is a great way to generate secure, random, and long passwords.
It’s a great strategy for your most precious passwords (e.g. the password to your computer, your backups, or your encryption key).
You can even use Diceware to create secure wallets.

To generate a password using Diceware, you just need a good die and some pen and paper.
You can find the diceware list at the [Electronic Frontier Foundation website](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases).
Make sure you are alone and there are no cameras nearby.
For maximum protection, disconnect your computer from the internet (after you save the Diceware list) and cover your webcam.

To start, roll the die five times.
Record the number from each roll using the pen and paper.
You will end up with a five-digit number.
We got `52611`.
Now search on the Diceware list for the five digit number you just created.
Write down the word the number corresponds to, in our case it is `salvo`.
This word by itself is not a good password, it would only take about a thousandth of a second to crack.
Repeat the dice rolling process at least, four times.

After five sets of five rolls, we ended up with `52611` `51631` `63432` `43123` `21641`.
This corresponds to the password `salvo rhoda walton mudd croft`.

It would take a single computer about six nonillion (which is 6*10^30 ) years to crack this.
It is an unimaginably large number and for comparison, the universe is only 14 x 10 to the power of 9 years old.
If you had a billion computers, each one a billion times stronger than the computers available today, you would still not be able to crack this password.
Keep a [secure backup](/using-wasabi/ColdWasabi.md#a-list-of-the-more-common-mediums-of-cold-storage-with-some-of-their-weaknesses) of the password, but store it in a separate location from your main 12 recovery words.

## How are the secrets created

Wasabi uses [BIP 38: Password-Protected Private Key](/using-wasabi/BIPs.md#bip-38-password-protected-private-key)

```
                      +--------------+
                      | Entropy      |
                      +--------------+
  +------------+             |
  | Word list  +------------>+
  +------------+             |
                      +------v-------+
                      | Mnemonics    |
                      +--------------+
                             |
                   +--------->
                   |         |
                   |  +------v-------+
                   |  | Seed         |
                   |  +--------------+
                   |         |
   +-----------+   |         |
   | Password  +---+  +------v-------+
   +-----------+   |  | Extended Key |
                   |  +--------------+
                   |         |
                   |         |
                   |  +------v-------+
                   |  | Private key  |     ** This step is needed to use bip38
                   |  +--------------+
                   |         |              +-------------+
                   +-------->+<-------------+  Network    |
                             |              +-------------+
                      +------v-------+
                      | Encrypted    |
                      | secret       |
                      +--------------+
                             |
                             |
                             |
                  +--------------------+
                  | Save encrypted     |
                  | secret+chaincode+  |
                  | Fingerprint+ExtPub |
                  +--------------------+

```
