 # Collect CSV 

## Access

Windows (WF):

### Conception :

> TYPE MOT DE PASSE : 
```c#
 public enum PassWordType
    {
        Aléatoire,
        Construit
    }
```

> Lors de la création d'un élève, on sait s'il s'agit d'un mdp construit ou aléatoire grâce au type : 
```c#
 public Eleve(int _idClasse, string _nom, string _prenom, string _login, bool _passWord, int _idAuth)
        {
            this.idClasse = _idClasse;
            this.nom = _nom;
            this.prenom = _prenom;
            this.login = _login;
            this.idAuth = _idAuth;
            this.passWord = GetNewPassWord(_passWord);
        }
```
**this.passWord = GetNewPassWord(_passWord);** : 

```c#
 private string GetPassWordConstruit()
        {
            string passWord = "";
            passWord = prenom.Substring(0, 1) + nom;
            return passWord;
        }
```

> Hachage : 
```c#
    private string Sha264(string passWord)
        {
            var message = Encoding.ASCII.GetBytes(passWord);
            SHA256Managed hashString = new SHA256Managed();
            string hex = "";
            // rajouter l'id. 
            var hashValue = hashString.ComputeHash(message);
            foreach (byte x in hashValue)
            {
                hex += String.Format("{0:x2}", x);
            }
            return hex;
        }

        private string Salt(string passWord, int size)
        {
            var random = new RNGCryptoServiceProvider();
            // Maximum length of salt
            int max_length = 32;
            // Empty salt array
            byte[] salt = new byte[max_length];
            // Build the random bytes
            random.GetNonZeroBytes(salt);
            // Return the string encoded salt
            return Convert.ToBase64String(salt);
        }
```
Le chiffrement SHA256 calcule une empreinte numérique de 256 bits soit 32 octets, dont l'écriture hexadécimale comprend 64 caractères. L'algorithme utilise des fonctions non linéaires comme :
## Meta

Bourdon Maxime – Mbourdon.pro@gmail.com

[https://github.com/Mbourdon95/github-link](https://github.com/Mbourdon95/)
 
 
 
    logging.info("STORED AT : "+ TARGET_DIRECTORY +"_temperature_{}.csv".format(DATE))

