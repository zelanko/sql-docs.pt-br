---
title: Gerenciando senhas (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/05/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 56d546e3-8747-4169-aace-693302667e94
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b5be535275742efa87dec804e17a94ef6cc8d092
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000163"
---
# <a name="managing-passwords-db2tosql"></a>Gerenciando senhas (DB2ToSQL)
Esta seção trata da proteção de senhas de banco de dados e do procedimento para importá-las ou exportá-las entre servidores:  
  
1.  Protegendo a senha  
  
2.  Exportando ou importando senha criptografada  
  
## <a name="securing-password"></a>Protegendo a senha  
O SSMA permite que você proteja sua senha de um banco de dados.  
  
Use o procedimento a seguir para implementar uma conexão segura:  
  
Especifique uma senha válida usando um dos três métodos a seguir:  
  
1.  **Texto não criptografado:** Digite a senha do banco de dados no atributo Value do nó ' password '. Ele é encontrado no nó definição do servidor na seção servidor do arquivo de script ou arquivo de conexão do servidor.  
  
    As senhas em texto não criptografado não são seguras. Portanto, você encontrará a seguinte mensagem de aviso na saída do console: *"servidor Server &lt; -ID &gt; da senha é fornecido em formato de texto não seguro, o aplicativo do console do SSMA fornece uma opção para proteger a senha por meio de criptografia, consulte a opção-SecurePassword no arquivo de ajuda do SSMA para obter mais informações".*  
  
    **Senhas criptografadas:** A senha especificada, nesse caso, é armazenada em um formato criptografado no computador local no ProtectedStorage. SSMA.  
  
    -   **Protegendo senhas**  
  
        -   Execute o `SSMAforDB2Console.exe` com o `-securepassword` e adicione a opção na linha de comando passando a conexão do servidor ou o arquivo de script que contém o nó senha na seção definição do servidor.  
  
        -   No prompt, o usuário será solicitado a inserir a senha do banco de dados e confirmá-la.  
  
            As IDs de definição de servidor e suas senhas criptografadas correspondentes são armazenadas em um arquivo no computador local  
            
            Exemplo 1:
            
                Specify password
                C:\SSMA\SSMAforDB2Console.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Exemplo 2:
            
                C:\SSMA\SSMAforDB2Console.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Removendo senhas criptografadas**  
  
        Execute o `SSMAforDB2Console.exe` com a `-securepassword` `-remove` opção e na linha de comando passando as IDs do servidor, para remover as senhas criptografadas do arquivo de armazenamento protegido presente no computador local.  
  
        Exemplo:  

        ```console
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -remove all
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -remove "source_1,target_1"
        ```

    -   **Listando IDs de servidor cujas senhas são criptografadas**  
  
        Execute o `SSMAforDB2Console.exe` com a `-securepassword` `-list` opção e na linha de comando para listar todas as IDs de servidor cujas senhas foram criptografadas.  
  
        Exemplo:  

        ```console
        C:\SSMA\SSMAforDB2Console.EXE -securepassword -list
        ```

    > [!NOTE]  
    > 1.  A senha em texto não criptografado mencionado no arquivo de conexão de script ou servidor tem precedência sobre a senha criptografada no arquivo protegido.  
    > 2.  Quando não houver nenhuma senha na seção do servidor do arquivo de conexão do servidor ou do arquivo de script ou se não tiver sido protegida no computador local, o console do solicitará que você insira a senha.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportando ou importando senhas criptografadas  
O aplicativo de console do SSMA permite exportar senhas de banco de dados criptografadas presentes em um arquivo no computador local para um arquivo protegido e vice-versa. Ele ajuda a tornar o computador com senhas criptografadas independente.

A _funcionalidade de exportação_ lê a ID do servidor e a senha do armazenamento protegido local. Em seguida, o sistema salva a ID e a senha em um arquivo criptografado. O usuário é solicitado a inserir a senha para o arquivo protegido. Verifique se a senha digitada tem 8 ou mais caracteres de comprimento. Esse arquivo protegido é portável em computadores diferentes.

A _funcionalidade de importação_ lê a ID do servidor e as informações de senha do arquivo protegido. O usuário é solicitado a inserir a senha para o arquivo protegido e anexa as informações ao armazenamento protegido local.  

### <a name="export-example"></a>Exemplo de exportação

1. Exporte a senha.

2. Insira a senha para proteger o arquivo exportado.

3. Executar: &nbsp;`C:\SSMA\SSMAforDB2Console.EXE -securepassword -export all "machine1passwords.file"`

4. Insira a senha para proteger o arquivo exportado: xxxxxxxx

5. Confirme a senha: xxxxxxxx

6. Executar: &nbsp;`C:\SSMA\SSMAforDB2Console.EXE -p -e "DB2DB_1_1,Sql_1" "machine2passwords.file"`

7. Insira a senha para proteger o arquivo exportado: xxxxxxxx

8. Confirme a senha: xxxxxxxx  

### <a name="import-example"></a>Exemplo de importação

1. Importar uma senha criptografada.

2. Insira a senha para proteger o arquivo importado.

3. Executar: &nbsp;`C:\SSMA\SSMAforDB2Console.EXE -securepassword -import all "machine1passwords.file"`

4. Insira a senha para importar os servidores do arquivo criptografado: xxxxxxxx

5. Confirme a senha: xxxxxxxx

6. Executar: &nbsp;`C:\SSMA\SSMAforDB2Console.EXE -p -i "DB2DB_1,Sql_1" "machine2passwords.file"`

7. Insira a senha para importar os servidores do arquivo criptografado: xxxxxxxx

8. Confirmar senha: xxxxxxxx

## <a name="see-also"></a>Consulte Também  
[Executar o console do SSMA](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
