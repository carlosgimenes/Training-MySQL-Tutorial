# **Training Leitura Livro - MySQL Tutorial: Uma Introdução Objetiva aos Fundamentos do Banco de Dados MySQL**

## Configuração Laboratório Treinamento

### Processo de criação da VM

1. Registrar no Controle VirtualBox (Planilha Apontamentos, Guia VirtualBox)
2. Definir IP fixo ou DHCP
3. Clonar com base em um Template
4. Ajustar informações na Descrição da VM
5. Iniciar a VM em modo Headless
6. Conectar na VM via SSH utilizando etiqueta do Template
7. Ajustar IP em `ConfigurarRedeComIpFixo.sh`
8. Executar `ConfigurarRedeComIpFixo.sh` para efetivar alteração do IP
9. Criar entrada no Remmina para a VM
10. Renomear o hostname
11. Efetuar update & upgrade

## Instalação do MySQL

### Download do MySQL

- [Link para Página de Download MySQL](https://dev.mysql.com/downloads/mysql/)

- Versão baixada: 8.4.3 LTS "DEB Bundle" para Ubuntu 20.04 (inclui todos os pacotes necessários).

### Checksums

- Site:

```text
8e645a96ce624fa9cf0bc8adc487422c
```

- Verificar checksum do arquivo baixado:

```bash
md5sum mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar
```

- Retorno esperado:

```text
8e645a96ce624fa9cf0bc8adc487422c
```

### Transferindo o arquivo baixado para a VM

#### No Host

```bash
scp mysql-community-server_8.4.3-1ubuntu24.04_amd64.deb username@192.168.0.xxx:/tmp
```

#### Na VM

```bash
cd /tmp
mv mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar /home/username/
cd /home/username/
```

### Instalação

Baseado no passo a passo descrito em:

- [Guia de Instalação](https://dev.mysql.com/doc/refman/8.4/en/linux-installation-debian.html)

Como eu fiz:

```bash
cd /home/username/
tar -xvf mysql-server_8.4.3-1ubuntu24.04_amd64.deb-bundle.tar
sudo apt-get install libaio1
sudo dpkg-preconfigure mysql-community-server_*.deb
sudo dpkg -i mysql-{common,community-client-plugins,community-client-core,community-client,client,community-server-core,community-server,server}_*.deb
sudo apt-get -f install
# Definir senha para root: Minh@Senh@123
sudo reboot
sudo systemctl status mysql
```

### Primeira conexão

```bash
mysql -u root -p
# Senha: Minh@Senh@123
```

### Criar usuário: `username`

**Sintaxe:**

1. **Criar o usuário**

```sql
CREATE USER 'username'@'%' IDENTIFIED BY 'MinhaSenha123';
```

2. **Conceder privilégios**

```sql
GRANT CREATE, CREATE TEMPORARY TABLES, DELETE, EXECUTE, INDEX, INSERT, LOCK TABLES, SELECT, SHOW DATABASES, UPDATE ON *.* TO 'username'@'%';
```

3. **Aplicar mudanças**

```sql
FLUSH PRIVILEGES;
```

4. **Testar o acesso**

```bash
mysql -u username -p
# Senha: MinhaSenha123
```

---

#### Teste