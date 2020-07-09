---
title: Gerenciando senhas (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/07/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Managing Passwords in Oracle, Exporting or Importing Encrypted Password
- Managing passwords in Oracle, Securing Password
ms.assetid: 8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a3fe98b4a0b552d8c26d64eed777d5bcadc42cd7
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159994"
---
# <a name="managing-passwords-oracletosql"></a>Gerenciar senhas (OracleToSQL)
Esta seção trata da proteção de senhas de banco de dados e do procedimento para importá-las ou exportá-las entre servidores.

## <a name="securing-password"></a>Protegendo a senha  
O SSMA permite que você proteja sua senha de um banco de dados.  
  
Use o procedimento a seguir para implementar uma conexão segura:  
  
Especifique uma senha válida usando um dos três métodos a seguir:  
  
1.  **Texto não criptografado:** Digite a senha do banco de dados no atributo Value do nó ' password '. Ele é encontrado no nó definição do servidor na seção servidor do arquivo de script ou arquivo de conexão do servidor.  
  
    As senhas em texto não criptografado não são seguras. Portanto, você encontrará a seguinte mensagem de aviso na saída do console: *"servidor Server &lt; -ID &gt; da senha é fornecido em formato de texto não seguro, o aplicativo do console do SSMA fornece uma opção para proteger a senha por meio de criptografia, consulte a opção-SecurePassword no arquivo de ajuda do SSMA para obter mais informações".*  
  
    **Senhas criptografadas:** A senha especificada, nesse caso, é armazenada em um formato criptografado no computador local no ProtectedStorage. SSMA.  
  
    -   **Protegendo senhas**  
  
        -   Execute o `SSMAforOracleConsole.exe` com o `-securepassword` e adicione a opção na linha de comando passando a conexão do servidor ou o arquivo de script que contém o nó senha na seção definição do servidor.  
  
        -   No prompt, o usuário será solicitado a inserir a senha do banco de dados e confirmá-la.  
  
            As IDs de definição de servidor e suas senhas criptografadas correspondentes são armazenadas em um arquivo no computador local  
            
            Exemplo 1:  
            
            1. Especificar senha
                
            2. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml"`
                
            3. Insira a senha para o server_id ' XXX_1 ': xxxxxxx
                
            4. Digite a senha novamente para server_id ' XXX_1 ': xxxxxxx
            
            Exemplo 2:
            
            1. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml" -o`

            2. Insira a senha para o server_id ' source_1 ': xxxxxxx

            3. Digite a senha novamente para server_id ' source_1 ': xxxxxxx

            4. Insira a senha para o server_id ' target_1 ': xxxxxxx

            5. Digite a senha novamente para server_id ' target _1 ': xxxxxxx  
    
    -   **Removendo senhas criptografadas**  
  
        Execute o `SSMAforOracleConsole.exe` com a `-securepassword` `-remove` opção e na linha de comando passando as IDs do servidor, para remover as senhas criptografadas do arquivo de armazenamento protegido presente no computador local.  
        
        Exemplo:  

        ```console
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove all
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove "source_1,target_1"  
        ```

    -   **Listando IDs de servidor cujas senhas são criptografadas**  
  
        Execute o `SSMAforOracleConsole.exe` com a `-securepassword` `-list` opção e na linha de comando para listar todas as IDs de servidor cujas senhas foram criptografadas.  
  
        Exemplo:  

        ```console
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -list  
        ```
  
    > [!NOTE]  
    > 1.  A senha em texto não criptografado mencionado no arquivo de conexão de script ou servidor tem precedência sobre a senha criptografada no arquivo protegido.  
    > 2.  Quando não houver nenhuma senha na seção do servidor do arquivo de conexão do servidor ou do arquivo de script ou se não tiver sido protegida no computador local, o console do solicitará que você insira a senha.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportando ou importando senhas criptografadas  
O aplicativo de console do SSMA permite exportar senhas de banco de dados criptografadas presentes em um arquivo no computador local para um arquivo protegido e vice-versa. Ele ajuda a tornar o computador com senhas criptografadas independente. A funcionalidade de exportação lê a ID do servidor e a senha do armazenamento protegido local e salva as informações em um arquivo criptografado. O usuário é solicitado a inserir a senha para o arquivo protegido. Certifique-se de que a senha inserida tenha um comprimento de 8 caracteres ou mais. Esse arquivo protegido é portável em computadores diferentes. A funcionalidade de importação lê a ID do servidor e as informações de senha do arquivo protegido. O usuário é solicitado a inserir a senha para o arquivo protegido e acrescenta as informações ao armazenamento protegido local.  
  
### <a name="export-example"></a>Exemplo de exportação:  

1. Exportar senha

2. Insira a senha para proteger o arquivo exportado

3. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -export all "machine1passwords.file"`

4. Insira a senha para proteger o arquivo exportado: xxxxxxxx

5. Confirme a senha: xxxxxxxx

6. `C:\SSMA\SSMAforOracleConsole.EXE -p -e "OracleDB_1_1,Sql_1" "machine2passwords.file"`

7. Insira a senha para proteger o arquivo exportado: xxxxxxxx

8. Confirme a senha: xxxxxxxx  

### <a name="import-example"></a>Exemplo de importação:  

1. Importar uma senha criptografada

2. Insira a senha para proteger o arquivo importado

3. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -import all "machine1passwords.file"`

4. Insira a senha para importar os servidores do arquivo criptografado: xxxxxxxx

5. Confirme a senha: xxxxxxxx

6. `C:\SSMA\SSMAforOracleConsole.EXE -p -i "OracleDB_1,Sql_1" "machine2passwords.file"`

7. Insira a senha para importar os servidores do arquivo criptografado: xxxxxxxx

8. Confirme a senha: xxxxxxxx  

## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
