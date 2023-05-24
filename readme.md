# Exercises Ansible

Code for testing Given Ansible exercise below.

```yaml
ansible-playbook -i inventory.ini playbook.yml --extra-vars "@vars_scenario[number].yml"

or

ansible-playbook -i inventory.ini playbook.yml --extra-vars "target='ip_fedora' directories=['/opt/data1', '/opt/data3']"
ansible-playbook -i inventory.ini playbook.yml --extra-vars "target='ip_fedora' directories=['/opt/data4', '/opt/data5']"
ansible-playbook -i inventory.ini playbook.yml --extra-vars "target='ip_willekeurig' directories=['/opt/data1', '/opt/data2']"
```


## Exercise 1
 
Op Fedora VM maak de volgende directorystructuur aanmaken (inhoud mag willekeurige tekst zijn)?
/opt/data1/bestanda.txt
/opt/data1/bestandb.txt
/opt/data2/bestandc.txt
/opt/data2/bestandd.txt
/opt/data3/bestande.txt
/opt/data3/bestandf.txt

En dan op je Ubuntu VM kijken of je een playbook aan kunt maken dat:
Extra variabelen gebruikt als input:
    i.      Een lijst met directories

    ii.      Een machine waar data van gedownload moet worden (mag een IP adres zijn in deze situatie, weet niet hoe VirtualBox met DNS intern om gaat)

Controleert of de machine (opgegeven bij 2a.ii in de extra variabelen) te bereiken is, en de play stopt en een debug message weergeeft met “Systeem is niet te bereiken” (normaliter zou ik hier email voor pakken maar dat is op jouw testsysteem nog niet geconfigureerd)

Als de machine bereikbaar is gaat kijken of de directories opgegeven bij 2a.i ook bestaan op het systeem, en de play stopt en een debug message weergeeft met “Volgende directories kunnen op doelsysteem niet gevonden worden: {{ lijst_met_niet_gevonden_directories }}”
Als de directies bestaan deze inclusief inhoud naar je ubuntu machine in directory /opt/backup/{{ datum in formaat 2023-05-11, oftewel YYYY-mm-DD }}/{{ VM naam / IP adres }} kopieert
 

Testing scenario’s:

Aanroep script op Ubuntu machine met extra variabelen “target: IP_adres_van_fedora_machine, directories: [ /opt/data1, /opt/data3 ]” => zou succesvol moeten draaien en data1 en data3 wel over moeten zetten, data2 niet
Aanroep script op Ubuntu machine met extra variabelen “target: IP_adres_van_fedora_machine, directories: [ /opt/data4, /opt/data5 ]” => moet falen (directories bestaan niet)
Aanroep script op Ubuntu machine met extra variabelen “target: willekeurig_IP_adres, directories: [ /opt/data1, /opt/data2 ]” => moet falen (systeem is niet bereikbaar)