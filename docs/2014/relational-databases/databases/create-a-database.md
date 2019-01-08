---
title: Criar um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f527d9767a6e821d0d4d5527fcad70e37f16e3c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799108"
---
# <a name="create-a-database"></a>Criar um banco de dados
  Este tópico descreve como criar um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para criar um diagrama de banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
  
-   No máximo 32.767 bancos de dados podem ser especificados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   A instrução CREATE DATABASE deve ser executada em modo de confirmação automática (o modo padrão de gerenciamento de transações) e não é permitida em uma transação explícita ou implícita.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   O backup do banco de dados [mestre](master-database.md) deve ser feito sempre que um banco de dados de usuário for criado, modificado ou descartado.  
  
-   Ao criar um banco de dados, torne os arquivos de dados tão grandes quanto possível, com base na quantidade máxima de dados que você espera ter no banco de dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão CREATE DATABASE no banco de dados mestre, ou requer a permissão CREATE ANY DATABASE ou ALTER ANY DATABASE.  
  
 Para manter controle sobre o uso do disco em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a permissão para criar bancos de dados geralmente é limitada a algumas contas de logon.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-database"></a>Para criar um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Clique com o botão direito do mouse em **Bancos de Dados**e clique em **Novo Banco de Dados**.  
  
3.  Em **Novo Banco de Dados**, digite um nome de banco de dados.  
  
4.  Para criar o banco de dados aceitando todos os valores padrão, clique em **OK**; do contrário, passe para as etapas opcionais a seguir.  
  
5.  Para alterar o nome do proprietário, clique em (**...**) para selecionar outro proprietário.  
  
    > [!NOTE]  
    >  A opção **Usar indexação de texto completo** sempre está marcada e esmaecida porque, a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], todos os bancos de dados de usuários são habilitados para texto completo.  
  
6.  Para alterar os valores padrão dos arquivos de dados primários e de log de transação, na grade **Arquivos de banco de dados** , clique na célula apropriada e digite o novo valor. Para obter mais informações, consulte [adicionar dados ou arquivos de Log para um banco de dados](add-data-or-log-files-to-a-database.md).  
  
7.  Para alterar a ordenação do banco de dados, selecione a página **Opções** e depois marque uma ordenação na lista.  
  
8.  Para alterar o modelo de recuperação, selecione a página **Opções** e marque um modelo de recuperação na lista.  
  
9. Para alterar opções de banco de dados, selecione a página **Opções** e depois modifique as opções de banco de dados. Para obter uma descrição de cada opção, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
10. Para adicionar um novo grupo de arquivos, clique na página **Grupos de Arquivos** . Clique em **Adicionar** e, em seguida, digite os valores para o grupo de arquivos.  
  
11. Para adicionar uma propriedade estendida ao banco de dados, selecione a página **Propriedades Estendidas** .  
  
    1.  Na coluna **Nome** , digite um nome para a propriedade estendida.  
  
    2.  Na coluna **Valor** , digite o texto da propriedade estendida. Por exemplo, digite uma ou mais instruções que descrevem o banco de dados.  
  
12. Para criar o banco de dados, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-create-a-database"></a>Para criar um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria o banco de dados `Sales`. Como a palavra-chave PRIMARY não é usada, o primeiro arquivo (`Sales`_`dat`) torna-se o arquivo primário. Como nem MB nem KB é especificado no parâmetro SIZE do arquivo `Sales`\_`dat` , ele usa MB e é alocado em megabytes. O backup do banco de dados `Sales`\_`log` é alocado em megabytes porque o sufixo `MB` é explicitamente declarado no parâmetro `SIZE` .  
  
```tsql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 Para obter mais exemplos, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos e grupos de arquivos do banco de dados](database-files-and-filegroups.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Adicionar arquivos de dados ou de log a um banco de dados](add-data-or-log-files-to-a-database.md)  
  
  
