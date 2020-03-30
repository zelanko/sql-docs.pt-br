---
title: Scripts nos testes de unidade do SQL Server
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 80c5cf62-a9c9-4e9d-8c6f-8eed50a595a7
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c5ff8457d5e2122f3e5bc455c204a5185cc30aec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75256975"
---
# <a name="scripts-in-sql-server-unit-tests"></a>Scripts nos testes de unidade do SQL Server

Cada teste de unidade do SQL Server contém uma única ação de pré-teste, ação de teste e ação de pós-teste. Cada uma dessas ações contém o seguinte:  
  
-   Um script Transact\-SQL executado em um banco de dados.  
  
-   Zero ou mais condições de teste que avaliam os resultados retornados pela execução do script.  
  
O script de teste Transact\-SQL na ação de teste é o único componente que você deve incluir em cada teste de unidade do SQL Server. Além do próprio script de teste, você provavelmente também precisará especificar condições de teste para verificar se o script de teste retornou o valor ou conjunto de valores esperado. A ação de teste exercita ou altera um objeto específico nesse banco de dados e avalia a alteração.  
  
Para cada ação de teste, você pode incluir uma ação de pré-teste e uma ação de pós-teste. Semelhante à ação de teste, cada ação de pré-teste e cada ação de pós-teste contém um script Transact\-SQL e zero ou mais condições de teste. Você pode usar uma ação de pré-teste para verificar se o banco de dados está em um estado que permite que sua ação de teste seja executada e retorne resultados significativos. Por exemplo, você pode usar uma ação de pré-teste para verificar se uma tabela contém dados antes de um script de teste realizar uma operação nesses dados. Depois que a ação de pré-teste prepara o banco de dados e retorna resultados significativos, a ação de pós-teste pode ser usada para retornar o banco de dados ao estado em que ele estava antes da execução da ação de pré-teste. Ou, em alguns casos, talvez seja necessário usar a ação de pós-teste para validar os resultados da ação de teste. Isso acontece porque a ação de pós-teste pode ter maiores privilégios de banco de dados do que a ação de teste. Para obter mais informações, consulte [Visão geral das cadeias de conexão e permissões](../ssdt/overview-of-connection-strings-and-permissions.md).  
  
Além dessas três ações, também há dois scripts de teste (conhecidos como scripts comum), que são executados antes e depois de cada execução de teste de unidade do SQL Server. Como resultado, até cinco scripts Transact\-SQL podem ser executados durante a execução de um único teste de unidade do SQL Server. Somente o script Transact\-SQL contido na ação de teste é necessário; os scripts comuns e os scripts de ação de pré-teste e de pós-teste são opcionais.  
  
A tabela a seguir fornece uma lista completa de scripts que são associados a qualquer teste de unidade do SQL Server.  
  
|**Ação**|**Tipo de script**|**Descrição**|  
|--------------|-------------------|-------------------|  
|TestInitialize|Script comum (inicialização)|(Opcional) Este script precede todas as ações de pré-teste e de teste no teste de unidade. O script TestInitialize é executado antes de cada teste de unidade em uma classe de teste específica. Ele é executado com o contexto privilegiado.|  
|Pré-teste|Script de teste|(Opcional) Este script faz parte do teste de unidade. O script de pré-teste é executado antes da ação de teste em um teste de unidade. Ele é executado com o contexto privilegiado.|  
|Teste|Script de teste|(Obrigatório) Este script faz parte do teste de unidade. Esse script pode, por exemplo, executar um procedimento armazenado que obtém, insere ou atualiza valores de tabela. Ele é executado com o contexto de execução.|  
|Pós-teste|Script de teste|(Opcional) Este script faz parte do teste de unidade. O script de pós-teste é executado após um teste de unidade individual. Ele é executado com o contexto privilegiado.|  
|TestCleanup|Script comum (limpeza)|(Opcional) Este script vem depois do teste de unidade. O script TestCleanup é executado após todos os testes de unidade de uma classe de teste específica. Ele é executado com o contexto privilegiado.|  
  
Para saber mais sobre os diferentes contextos de segurança nos quais cada um desses scripts é executado, confira [Visão geral das cadeias de conexão e permissões](../ssdt/overview-of-connection-strings-and-permissions.md) e a seção de permissões de teste de unidade do SQL Server em [Permissões necessárias para SQL Server Data Tools](../ssdt/required-permissions-for-sql-server-data-tools.md).  
  
## <a name="order-in-which-scripts-are-run"></a>Ordem na qual os scripts são executados  
É importante compreender a ordem em que cada script é executado. Embora você não possa alterar essa ordem, pode decidir quais scripts serão executados. A ilustração a seguir inclui a seleção dos scripts que você pode usar em uma execução de teste que contém dois testes de unidade do SQL Server e mostra a ordem na qual eles são executados:  
  
![Dois testes de unidade de banco de dados](../ssdt/media/twodatabaseunittests.png "Dois testes de unidade de banco de dados")  
  
> [!NOTE]  
> Se a implantação do projeto de banco de dados do SQL Server tiver sido configurada, isso ocorrerá no início da execução de teste, na cadeia de conexão de contexto privilegiado. Para obter mais informações, consulte [Como: Configurar a execução do teste de unidade do SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md).  
  
## <a name="initialization-and-cleanup-scripts"></a>Scripts de inicialização e de limpeza  
No Designer de Teste de Unidade do SQL Server, os scripts TestInitialize e TestCleanup são denominados scripts comuns. O exemplo anterior pressupõe que os dois testes de unidade fazem parte da mesma classe de teste. Como resultado, eles compartilham os mesmos scripts TestInitialize e TestCleanup. Essa condição é válida para todos os testes de unidade de uma única classe de teste. Entretanto, se a execução do teste contiver testes de unidade de classes de teste diferentes, os scripts comuns da classe de teste associada serão executados antes e depois da execução do teste de unidade.  
  
Se você gravar os testes de unidade usando apenas o Designer de Teste de Unidade do SQL Server, possivelmente não se familiarizará com o conceito de uma classe de teste. Cada vez que você cria um teste de unidade abrindo menu **Teste** e clicando em **Novo Teste**, o SQL Server Data Tools gera uma classe de teste. As classes de teste são exibidas no **Gerenciador de Soluções** com o nome de teste especificado, seguido por uma extensão .cs ou .vb. Dentro de cada classe de teste, os testes de unidade individuais são armazenados como métodos de teste. No entanto, independentemente do número de métodos de teste (ou seja, testes de unidade), cada classe de teste pode ter zero ou um script TestInitialize e um script TestCleanup.  
  
Você pode usar o script TestInitialize para preparar o banco de dados de teste e o script TestCleanup para retornar o banco de dados de teste a um estado conhecido. Por exemplo, você pode usar TestInitialize para criar um procedimento armazenado auxiliar que será executado posteriormente, no script de teste, para testar um procedimento armazenado diferente.  
  
## <a name="pre-test-and-post-test-scripts"></a>Scripts de pré-teste e pós-teste  
Os scripts associados às ações de pré-teste e pós-teste provavelmente variarão de um teste de unidade para outro. Você pode usar esses scripts para estabelecer alterações incrementais no banco de dados e limpar essas alterações.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Usar condições de teste nos testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
  
