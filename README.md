# GNU-Linux-SSH-Atsiskaitymas

## Instrukcijos

Sukurti ekrano atvaizdus atliktų veiksmų, trumpai aprašyti ir įkelti "history" įvestų komandų. <br />
Visą darbą įkelti .docx formatu į Teams. <br />


Sukurti dvi virtualias mašinas: <br />
Kali Linux ir Ubuntu LTS. Ant abiejų mašinų paleisti lsb_release -a komandą. - 2 taškai <br />
Ant Ubuntu virtualios mašinos įdiegti OpenSSH serverį - 1 taškas <br />
Ant Kali Linux sugeneruoti ed25519 raktą su komentaru "Atsiskaitomasis Darbas" ir nusiųsti viešą raktą į Ubuntu LTS (Įkelti atvaizdus Public ir Private Key) - 2 taškai <br />
Padaryti pakeitimus serverio konfigūracijoje: - 4 taškai <br />
Išjungti Password Authentication <br />
Įjungti Public Key Authentication <br />
Pakeisti SSH port iš 22 į 42069 <br />
Pabandyti prisijungti prie sistemos - 1 taškas <br />

<br />
<br />

`lsb_release -a` komandos rezultatas <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/lsb-release-ubuntu.JPG)

<br />

`lsb_release -a` komandos rezultatas <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/lsb-release-kali.JPG)

<br />

Su `sudo apt install openssh-server -y` komanda įsirašau OpenSSH serverį. `-y` parametras automatiškai sutinka papildomais package'ais, kurių gali prireikti <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/openssh-server-install.JPG)

<br />

Tada patikrinu ar serveris įsirašė su `apt list openssh-server --installed` komanda <br/>
Paleidžiu serverį su `sudo systemctl start ssh.service` ir patikrinu ar sėkmingai pasileido su `sudo systemctl status ssh.service` <br />
Ir pabaigoje pasitikrinu IP adresą su `ip addr` <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/openssh-server-init.JPG)

<br />

Sugeneruoju SSH raktą su `ssh-keygen -t ed25519 -f ~/.ssh/GNU-Linux-Atsiskaitymas -C "Atsiskaitomasis Darbas"` <br/>
`-t` nurodo koks algoritmas <br/>
`-f` nurodo failo vietą ir pavadinimą <br/>
`-C` nurodo komentarą <br/>
Tada patikrinu ar raktas teisingai susikūrė ir parodau public ir private raktų turinį

![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/ssh-keygen-kali.JPG)

<br />

Su `ssh-copy-id -i GNU-Linux-Atsiskaitymas ubuntu@192.168.1.134` perduodu public raktą serveriui <br/><br />
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/ssh-key-transfer.JPG)

<br />

Pasitikrinu su `cat .ssh/authorized_keys` ar serveris gavo public raktą <br/>
Pakeičiu serverio SSH konfiguraciją ir paleidžiu komandas `sudo systemctl daemon-reload` ir `sudo systemctl restart ssh.socket`, kad serveris pritaikytų naujus nustatymus <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/sshd-config.JPG)

<br/>

Galiausiai prisijungiu prie serverio pridedamas private raktą ir kitą portą <br/><br/>
![](https://github.com/deividasaldonis/GNU-Linux-SSH-Atsiskaitymas/blob/main/ssh-into-server.JPG)







