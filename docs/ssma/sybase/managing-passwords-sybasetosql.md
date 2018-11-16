---
title: Gerenciamento de senhas (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Exporting or Importing Encrypted Passwords
- Sybase Console,Managing Passwords
- Sybase Console,Securing Password
ms.assetid: 9b6a70f9-6840-4140-a059-bb7bd7ccc67c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a7df105a383cb7a647df1f26dbfc7793ae376df5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660155"
---
# <a name="managing-passwords-sybasetosql"></a>Gerenciamento de senhas (SybaseToSQL)
Esta seção é sobre como proteger as senhas de banco de dados e o procedimento para importar ou exportá-los entre servidores:  
  
1.  Proteção de senha  
  
2.  Exportar ou importar a senha criptografada  
  
## <a name="securing-password"></a>Proteção de senha  
O SSMA permite proteger sua senha de um banco de dados.  
  
Use o procedimento a seguir para implementar uma conexão segura:  
  
Especifique uma senha válida, usando um dos três métodos a seguir:  
  
1.  **Texto não criptografado:** digite a senha do banco de dados no atributo de valor do nó 'senha'. Ele é encontrado sob o nó de definição de servidor na seção de servidor do arquivo de script ou arquivo de conexão do servidor.  
  
    As senhas em texto não criptografado não são seguras. Portanto, você encontrará a seguinte mensagem de aviso na saída do console: *"servidor &lt;id do servidor&gt; senha é fornecida na forma de texto não criptografado não seguro, o aplicativo de Console do SSMA fornece uma opção para proteger o senha por meio da criptografia, consulte a opção – securepassword no SSMA arquivo de ajuda para obter mais informações."*  
  
    **Senhas criptografadas:** a senha especificada, nesse caso, é armazenada em um formato criptografado no computador local em ProtectedStorage.ssma.  
  
    -   **Proteger senhas**  
  
        -   Execute o `SSMAforSybaseConsole.exe` com o `–securepassword` e adicione o comutador na linha de comando, passando o servidor de conexão ou arquivo de script que contém o nó de senha na seção de definição de servidor.  
  
        -   No prompt, o usuário é solicitado a inserir a senha do banco de dados e confirmá-la.  
  
            As ids de definição de servidor e suas senhas criptografadas correspondentes são armazenadas em um arquivo no computador local  
            
            Exemplo 1:  
            
                Specify password
                
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Exemplo 2:
            
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Remover senhas criptografadas**  
  
        Execute o `SSMAforSybaseConsole.exe` com o`–securepassword` e `–remove` alternar na linha de comando, passando as ids do servidor, para remover as senhas criptografadas do armazenamento protegido arquivo presente no computador local.  
  
        Exemplo:  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **Listando as Ids do servidor cujas senhas são criptografadas**  
  
        Execute o `SSMAforSybaseConsole.exe` com o `–securepassword` e `–list` alternar na linha de comando para listar todas as ids do servidor cujas senhas foram criptografadas.  
  
        Exemplo:  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  A senha em texto não criptografado mencionado no arquivo de conexão de servidor ou de script tem precedência sobre a senha criptografada no arquivo protegido.  
    > 2.  Quando nenhuma senha existe na seção servidor de arquivo de conexão do servidor ou o arquivo de script ou se ele não foram protegido no computador local, o console solicitará que você insira a senha.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportando ou importando senhas criptografadas  
O aplicativo de Console do SSMA permite que você exporte as senhas de banco de dados criptografado presente em um arquivo no computador local para um arquivo protegido e vice-versa. Ele ajuda a tornar a máquina de senhas criptografadas independentes. Funcionalidade de exportação lê a id do servidor e armazenamento protegido de senha no local e salva as informações em um arquivo criptografado. O usuário é solicitado a inserir a senha para o arquivo protegido. Verifique se a senha inserida é o comprimento de 8 caracteres ou mais. Esse arquivo protegido é portátil entre diferentes computadores. Funcionalidade de importação lê o servidor de informações de id e a senha do arquivo protegido. O usuário é solicitado a inserir a senha para o arquivo protegido e acrescenta as informações para o armazenamento local protegido.  
  
Exemplo:  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –e "SybaseDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
Exemplo:  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –i "SybaseDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (Sybasetosql)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
