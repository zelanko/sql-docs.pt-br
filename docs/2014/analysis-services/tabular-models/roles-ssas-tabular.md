---
title: Funções (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3748f99899990bd46379928b3d524e43e48d277a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019468"
---
# <a name="roles-ssas-tabular"></a>Funções (SSAS tabular)
  Funções, em modelos tabulares, definem permissões de membro para um modelo. Cada função contém membros, por nome de usuário do Windows ou grupo do Windows, e permissões (leitura, processo, administrador). Membros da função podem executar ações no modelo conforme definido pela permissão de função. As funções definidas com permissões de leitura também podem fornecer segurança adicional no nível de linha usando filtros no nível de linha.  
  
> [!IMPORTANT]  
>  Para que os usuários conectem-se a um modelo implantado usando uma relação ou aplicativo cliente de análise de dados, você deve criar pelo menos uma função com pelo menos permissão de leitura da qual esses usuários são os membros.  
  
 As informações neste tópico são destinadas a autores de modelos tabulares que definem funções usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. As funções definidas durante a criação do modelo aplicam-se ao banco de dados de espaço de trabalho do modelo. Depois que um modelo de banco de dados foi implantado, os administradores de modelo de banco de dados podem gerenciar (adicionar, editar, excluir) membros de função usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para saber sobre como gerenciar os membros de funções em um banco de dados implantado, consulte [Funções de modelo tabular &#40;SSAS Tabular&#41;](tabular-model-roles-ssas-tabular.md).  
  
 O [Modelagem Tabular &#40;Tutorial do Adventure Works&#41;](../tabular-modeling-adventure-works-tutorial.md) inclui informações adicionais e lições sobre como usar esse recurso.  
  
 Seções neste tópico:  
  
-   [Compreendendo funções](#bkmk_underst)  
  
-   [Permissões](#bkmk_permissions)  
  
-   [Filtros de linha](#bkmk_rowfliters)  
  
-   [Testando funções](#bkmk_testroles)  
  
-   [Tarefas relacionadas](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> Compreendendo funções  
 As funções são usadas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para gerenciar a segurança para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os dados. Existem dois tipos de funções no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   A função do servidor, uma função fixa que fornece acesso de administrador a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   As funções de banco de dados, funções definidas por autores e administradores do modelo para controlar o acesso a banco de dados modelo e dados para usuários não administradores.  
  
 As funções, definidas para um modelo de tabela, são funções de banco de dados. Ou seja, as funções contêm membros que consistem em usuários ou grupos do Windows que têm permissões específicas que definem a ação que esses membros podem realizar no banco de dados modelo. Uma função de banco de dados é criada como um objeto separado no banco de dados e aplica-se apenas ao banco de dados no qual a função foi criada. Os usuários do Windows e/ou grupos do Windows são incluídos na função pelo autor modelo, que, por padrão, tem permissões de Administrador no servidor de banco de dados de espaço de trabalho; para um modelo implantado, por um administrador.  
  
 As funções em modelos tabulares podem ser definidas posteriormente com filtros de linha. Os filtros de linha usam expressões DAX para definir as linhas em uma tabela, e as linhas relacionadas nas muitas direções, que um usuário pode consultar. Os filtros de linha que usam expressões DAX somente podem ser definidos para as permissões de Leitura e Leitura e Processo. Para obter mais informações, consulte [Row Filters](#bkmk_rowfliters) mais adiante neste tópico.  
  
 Por padrão, quando você cria um novo projeto de modelo de tabela, o projeto de modelo não tem nenhuma função. As funções podem ser definidas usando a caixa de diálogo Gerenciador de Funções no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Quando as funções são definidas durante a criação do modelo, elas são se aplicadas ao banco de dados de espaço de trabalho do modelo. Quando o modelo é implantado, as mesmas funções são aplicadas ao modelo implantado. Depois que um modelo foi implantado, os membros da função de servidor (Administrador do[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) e administradores de banco de dados podem gerenciar as funções associadas ao modelo e os membros associados a cada função usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  As funções definidas para um modelo configurado para o modo DirectQuery não podem usar filtros de linha, porém, as permissões definidas para cada função serão aplicadas.  
  
##  <a name="bkmk_permissions"></a> Permissões  
 Cada função tem uma única permissão de banco de dados definida (exceto para a permissão de Ler e Processar combinada). Por padrão, uma nova função terá a permissão Nenhum. Ou seja, quando os membros são adicionados à função com a permissão Nenhum, eles não podem modificar o banco de dados, executar uma operação de processo, consultar dados ou ver o banco de dados a menos que uma permissão diferente seja concedida.  
  
 Um grupo ou usuário do Windows pode ser um membro de qualquer número de funções, cada função com uma permissão diferente. Quando um usuário for um membro de várias funções, as permissões definidas para cada função serão cumulativas. Por exemplo, se um usuário for membro de uma função com permissão de leitura e também um membro de uma função com permissão Nenhum, ele terá permissão de leitura.  
  
 Cada função pode ter uma das seguintes permissões definidas:  
  
|Permissões|Description|Filtros de linha usando DAX|  
|-----------------|-----------------|----------------------------|  
|Nenhum|Os membros não podem fazer modificações ao esquema de banco de dados modelo e não podem consultar dados.|Filtros de linha não são aplicáveis. Os dados não são visíveis a usuários nesta função|  
|leitura|Os membros têm permissão de consultar dados (com base em filtros de linha), mas não podem ver o banco de dados modelo no SSMS, não podem fazer nenhuma alteração ao esquema de banco de dados modelo e o usuário não pode processar o modelo.|Os filtros de linha podem ser aplicados. Somente os dados especificados na fórmula DAX de filtro de linha são visíveis a usuários.|  
|Leitura e processo|Os membros têm permissão de consultar dados (com base em filtros em nível de linha) e executar operações de processo por meio de um script ou pacote que contém um comando de processo, mas não pode fazer nenhuma alteração ao banco de dados. Não pode exibir o banco de dados modelo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Os filtros de linha podem ser aplicados. Somente os dados especificados na fórmula DAX de filtro de linha possam ser consultados.|  
|Processar|Os membros podem executar operações de processo por meio de um script ou pacote que contém um comando de processo. Não pode modificar o esquema de banco de dados modelo. Não é possível consultar dados. Não pode consultar o banco de dados modelo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Filtros de linha não são aplicáveis. Nenhum dado pode ser consultado nesta função|  
|Administrador|Os membros podem fazer modificações ao esquema modelo e consultar todos os dados no designer de modelo, no cliente de relatório e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Filtros de linha não são aplicáveis. Todos os dados podem ser consultados nesta função.|  
  
##  <a name="bkmk_rowfliters"></a> Filtros de linha  
 Os filtros de linha definem quais linhas em uma tabela podem ser consultados por membros de uma função específica. Os filtros de linha são definidos para cada tabela em um modelo usando fórmulas DAX.  
  
 Os filtros de linha podem ser definidos somente para funções com permissões de Leitura e Leitura e Processo. Por padrão, se um filtro de linha não for definido para uma tabela específica, os membros de uma função que têm permissão de Leitura ou Leitura e Processo poderão consultar todas as linhas na tabela a menos que a filtragem cruzada seja aplicada de outra tabela.  
  
 Quando um filtro de linha é definido para uma tabela específica, uma fórmula DAX, que deve ser avaliada como um valor TRUE/FALSE, define as linhas que poderão ser consultadas por membros daquela função específica. As linhas não incluídas na fórmula DAX não poderão ser consultadas. Por exemplo, para membros da função de Vendas, a tabela Customers com a seguinte expressão de filtros de linha, *=Customers [Country] = “USA”*, os membros da função de Vendas só poderão consultar clientes nos EUA.  
  
 Os filtros de linha aplicam-se às linhas especificadas e também a linhas relacionadas. Quando uma tabela tiver várias relações, os filtros aplicam segurança para a relação que está ativa. Os filtros de linha serão intersectados com outros filtros de linha definidos para tabelas relacionadas, por exemplo:  
  
|Table|Expressão DAX|  
|-----------|--------------------|  
|Região|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|Transactions|=Transactions[Year]=2008|  
  
 O efeito líquido destas permissões na tabela de Transações é que os membros terão permissão de consultar as linhas de dados quando o cliente estiver nos EUA, e a categoria de produto for bicicletas e o ano for 2008. Os usuários não poderiam consultar nenhuma transação fora dos EUA ou nenhuma transação que não fosse bicicletas nem em 2008, a menos que fossem membros de outra função que concede estas permissões.  
  
 Você pode usar o filtro *=FALSE()* para negar acesso a todas as linhas para uma tabela inteira.  
  
### <a name="dynamic-security"></a>Segurança dinâmica  
 A segurança dinâmica é um modo de definir a segurança de nível de linha com base no nome de usuário do usuário conectado no momento ou a propriedade CustomData retornada de uma cadeia de conexão. A fim de implementar uma segurança dinâmica, você deve incluir em seu modelo uma tabela com valores de logon (nome de usuário do Windows) para usuários, assim como um campo que pode ser usado para definir uma permissão específica; por exemplo, uma tabela dimEmployees com uma ID de logon (domínio\nome de usuário) e também um valor de departamento para cada funcionário.  
  
 Para implementar uma segurança dinâmica, você pode usar as funções a seguir como parte de uma fórmula DAX para retornar o nome de usuário do usuário conectado atualmente ou a propriedade CustomData em uma cadeia de conexão:  
  
|Função|Description|  
|--------------|-----------------|  
|[Função USERNAME &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)|Retorna o domínio\ nome de usuário do usuário conectado atualmente.|  
|[Função CUSTOMDATA &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)|Retorna a propriedade CustomData em uma cadeia de conexão.|  
  
 Você pode usar a função LOOKUPVALUE para retornar valores para uma coluna na qual o nome de usuário do Windows seja igual ao nome de usuário retornado pela função USERNAME ou uma cadeia de caracteres retornada pela função CustomData. As consultas podem ser então restritas onde os valores retornados por LOOKUPVALUE correspondem a valores na mesma tabela ou na tabela relacionada.  
  
 Por exemplo, usando esta fórmula:  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 A função LOOKUPVALUE retorna valores para a coluna dimEmployees[DepartmentId] onde dimEmployees[LoginId] é igual ao LoginID do usuário conectado no momento, retornado por USERNAME, e os valores para dimEmployees[DepartmentId] são iguais aos valores para dimDepartmentGroup[DepartmentId]. Os valores em DepartmentId retornados por LOOKUPVALUE são usados para restringir as linhas consultadas na tabela dimDepartment, e as tabelas relacionadas por DepartmentId. Somente são retornadas as linhas onde DepartmentId também esteja nos valores para o DepartmentId retornados pela função LOOKUPVALUE.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> Testando funções  
 Ao criar um projeto de modelo, você pode usar o recurso Analisar no Excel para testar a eficácia das funções que você definiu. No menu **Modelo** no designer de modelo, quando você clica em **Analisar no Excel**, antes de o Excel abrir, a caixa de diálogo **Escolher Credenciais e Perspectiva** é aberta. Nesta caixa de diálogo, você pode especificar o nome de usuário atual, um nome de usuário diferente, uma função e uma perspectiva que você usará para se conectar ao modelo de espaço de trabalho como uma fonte de dados. Para obter mais informações, consulte [Analisar no Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Tarefas relacionadas  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criar e gerenciar funções &#40;Tabular do SSAS&#41;](create-and-manage-roles-ssas-tabular.md)|As tarefas neste tópico descrevem como criar e gerenciar funções usando a caixa de diálogo **Gerenciador de Funções** .|  
  
## <a name="see-also"></a>Consulte também  
 [Perspectivas &#40;Tabular do SSAS&#41;](perspectives-ssas-tabular.md)   
 [Analisar no Excel &#40;Tabular do SSAS&#41;](analyze-in-excel-ssas-tabular.md)   
 [Função USERNAME &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [Função LOOKUPVALUE &#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [Função CUSTOMDATA &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  