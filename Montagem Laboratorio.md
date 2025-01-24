# Training Leitura Livro - MySQL Tutorial Uma introdução objetiva aos fundamentos do banco de dados MySQL

## Configuração Laboratório Treinamento

### Processo de criação da VM

1.Registrar no Controle VirtualBox (Planilha Apontamentos, Guia VirtualBox)
2.Definir IP fixo ou DHCP
3.Clonar com base em um Template
4.Ajustar informações na Descrição da VM
5.Iniciar a VM em modo Headless
6.Conectar na VM via ssh utilizando etiqueta do Template
7.Ajustar IP em ```ConfigurarRedeComIpFixo.sh```
8.Executar ```ConfigurarRedeComIpFixo.sh``` para efetivar alteração do IP
9.Criar entrada no Remmina para a VM
10.Renomear o hostname
11.Efetuar update & upgrade

## Instalação do MySQL

### Download MySQL

- [Link para Página de Download MySQL](https://dev.mysql.com/downloads/mysql/)

- Baixado versão 8.4.3 LTS "DEB Bundle" para Ubuntu 20.04 (ela tem todos pacotes necessários).

### Checksums

- Site:
**8e645a96ce624fa9cf0bc8adc487422c**

- Check arquivo baixado

```bash
md5sum mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar
```

- Retorno:
**8e645a96ce624fa9cf0bc8adc487422c**

### Transferindo arquivo baixado para a VM

#### No Host

```bash
scp mysql-community-server_8.4.3-1ubuntu24.04_amd64.deb nomedousuario@192.168.0.xxx /tmp
```

#### Na VM

```bash
cd /tmp
mv mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar /home/nomedousuario/
cd /home/nomedousuario/
```

### Instalação

Utilizei como base o passo a passo descrito em:

- https://dev.mysql.com/doc/refman/8.4/en/linux-installation-debian.html

Como eu fiz:

```bash
cd /home/nomedousuario/
tar -xvf mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar
sudo apt-get install libaio1
sudo dpkg-preconfigure mysql-community-server_*.deb
sudo dpkg -i mysql-{common,community-client-plugins,community-client-core,community-client,client,community-server-core,community-server,server}_*.deb
sudo apt-get -f install
Senha para root: Minh@Senh@123
sudo reboot
sudo systemctl status mysql
```

#### Primeira conexão

```bash
mysql -u root -p
Senha: Minh@Senh@123
```

#### Criado usuário: ```nomedousuario```

**Sintaxe:**

1. **Crie o usuário**

```sql
CREATE USER 'nomedousuario'@'%' IDENTIFIED BY 'MinhaSenha123';
```

2. **Conceda os privilégios**

```sql
GRANT CREATE, CREATE TEMPORARY TABLES, DELETE, EXECUTE, INDEX, INSERT, LOCK TABLES, SELECT, SHOW DATABASES, UPDATE ON *.* TO 'nomedousuario'@'%';
```

3. **Aplique as mudanças**

```sql
FLUSH PRIVILEGES;
```

4. **Teste o acesso**

```bash
mysql -u nomedousuario -p
Senha: MinhaSenha123
```
