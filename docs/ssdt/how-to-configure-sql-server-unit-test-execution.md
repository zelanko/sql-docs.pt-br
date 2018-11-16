---
title: Como configurar a execução do teste de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: e0179429-13ce-4d23-ae27-e6419de0a575
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 45c7429dfc8824859b06ef16616b0b999a3f6fd0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666755"
---
# <a name="how-to-configure-sql-server-unit-test-execution"></a>Como: Configurar a execução do teste de unidade do SQL Server
Configurando o projeto de teste, você pode especificar várias configurações que determinam como os testes de unidade do SQL Server serão executados. Essas configurações são armazenados no arquivo app.config do projeto de teste. Se você editar esse arquivo diretamente, os novos valores aparecerão na caixa de diálogo Configuração de Teste.  
  
A solução pode conter vários projetos de teste. Cada projeto de teste contém um arquivo app.config (ou seja, um conjunto de configurações). Consequentemente, a solução pode conter diferentes conjuntos de testes de unidade (um para cada projeto de teste) configurados para serem executados de maneira diferente.  
  
Essas configurações determinam como o teste se conectará ao banco de dados a ser testado, como você implantará um esquema de um projeto de banco de dados nesse banco de dados:  
  
-   **Conexões de Banco de Dados**. Use essa configuração para especificar as cadeias de conexão usadas para se conectar ao banco de dados que você está testando. Para saber mais, confira [Especificar cadeias de conexão](#SpecifyConnectionStrings).  
  
-   **Implantação do esquema**. Um projeto de banco de dados é uma representação offline do banco de dados. O projeto de banco de dados representa a estrutura dos objetos de banco de dados, mas não contém nenhum dado. Depois que você fizer alterações no esquema em um projeto de banco de dados, poderá testá-los em um banco de dados real. Na etapa de implantação do esquema, os objetos de banco de dados que você deseja testar serão copiados do projeto de banco de dados para o banco de dados no qual você executará os testes. Para saber mais sobre implantação de esquema, confira [Implantar um esquema de banco de dados](#DeployingDBSchema).  
  
    > [!NOTE]  
    > Os testes não são executados na pasta de soluções, mas em uma pasta separada no disco rígido local. Embora seja possível configurar aspectos da implantação de teste, você normalmente não precisa configurá-los para os testes de unidade. Para saber mais sobre a implantação de teste, confira [Executar testes](https://msdn.microsoft.com/library/dd286680(VS.100).aspx).  
  
## <a name="SpecifyConnectionStrings"></a>Especificar cadeias de conexão  
  
#### <a name="to-specify-database-connection-strings"></a>Para especificar cadeias de conexão de banco de dados  
  
1.  Clique com o botão direito do mouse no projeto de teste de unidade no **Gerenciador de Soluções** e clique na **Configuração de teste do SQL Server**.  
  
    A caixa de diálogo **Configuração de Teste do SQL Server - '<projectname>'** é exibida.  
  
2.  Em **Conexões de Banco de Dados**, você pode fazer o seguinte:  
  
    -   Clique na conexão de banco de dados na qual deseja executar testes de unidade.  
  
    -   Marque a caixa de seleção **Usar uma conexão de dados secundária** para validar testes de unidade e clique em uma conexão de banco de dados na lista se quiser que a execução do teste seja validada em uma conexão de banco de dados diferente.  
  
    -   Clique em **Nova Conexão** para adicionar uma conexão a qualquer uma das listas. Você também pode clicar em **Editar Conexão** para modificar as configurações em uma conexão existente.  
  
    Essa etapa cria a cadeia de conexão `ExecutionContext`, que é usada para executar o script no teste de unidade. Se você também especificar uma conexão secundária, a cadeia de conexão `PrivilegedContext` também será criada. Essa conexão é usada para testar as interações com o banco de dados fora do script de teste no teste de unidade. Para obter mais informações, consulte [Visão geral das cadeias de conexão e permissões](../ssdt/overview-of-connection-strings-and-permissions.md).  
  
3.  Clique em **OK** para fechar a caixa de diálogo **Configuração de Teste do SQL Server -'<projectname>'**.  
  
4.  Recompile o projeto de teste para aplicar as alterações de configuração.  
  
## <a name="DeployingDBSchema"></a>Implantar um esquema de banco de dados  
  
#### <a name="to-deploy-to-a-database-the-schema-of-a-database-project"></a>Para implantar o esquema de um projeto de banco de dados em um banco de dados  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de banco de dados e clique em **Compilar**.  
  
    Quando você compilar o projeto de banco de dados, gerará um script Transact\-SQL. Esse script, quando executado em um banco de dados, recria a estrutura do projeto nesse banco de dados.  
  
2.  Selecione o projeto de teste a ser configurado.  
  
3.  Clique com o botão direito do mouse no projeto de teste de unidade no **Gerenciador de Soluções** e clique na **Configuração de teste do SQL Server**.  
  
    A caixa de diálogo **Configuração de Teste do SQL Server - '<projectname>'** é exibida.  
  
4.  Em **Implantação**, você pode fazer o seguinte:  
  
    -   Marque a caixa de seleção **Implantar automaticamente projetos de banco de dados antes de executar testes** para garantir que todas as alterações de esquema feitas no projeto de banco de dados serão confirmadas antes que os testes sejam executados.  
  
    -   Em **Projeto de Banco de Dados**, clique no projeto de banco de dados a ser implantado ou clique nas reticências para procurar outro projeto. Os arquivos do projeto de banco de dados têm a extensão .dbproj.  
  
    -   Em **Configuração da Implantação**, clique na configuração de projeto na qual deseja fazer a implantação. As escolhas são **Depurar**, **Padrão** ou **Versão**. No entanto, se você criar uma configuração para testes de unidade, ela também aparecerá como opção.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Configuração de Teste do SQL Server -'<projectname>'**.  
  
    No início da execução do teste, o script Transact\-SQL gerado na etapa 1 será executado. Essa ação implantará o esquema no banco de dados de destino.  
  
6.  Recompile o projeto de teste de unidade para aplicar as alterações de configuração.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
