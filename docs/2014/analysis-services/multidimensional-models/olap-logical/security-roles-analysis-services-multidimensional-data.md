---
title: Funções de segurança (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 979f6302d3b03a06187d3ed1860b3c167ff66828
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165517"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>Funções de Segurança (Analysis Services - Dados Multidimensionais)
  As funções são usadas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para gerenciar a segurança de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos e dados. Em termos básicos, uma função associa os identificadores de segurança (SIDs) de usuários do Microsoft Windows e grupos que têm direitos de acesso específicos e as permissões definidas para objetos gerenciados por uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Dois tipos de funções são fornecidos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:  
  
-   A função do servidor, uma função fixa que fornece acesso de administrador a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   As funções de banco de dados, funções definidas por administradores para controlar o acesso a objetos e dados para usuários não administradores.  
  
 Segurança no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] segurança é gerenciada por meio de funções e permissões. As funções são grupos de usuários. Os usuários, também chamados de membros, podem ser adicionados ou removidos das funções. Permissões para objetos são especificadas por funções e todos os membros em uma função podem usar os objetos para o qual tem permissão. Todos os membros em uma função têm permissões iguais para os objetos. As permissões são específicas dos objetos. Cada objeto tem um conjunto de permissões concedidas para esse objeto; diferentes conjuntos de permissões podem ser concedidos para um objeto. Cada permissão, do conjunto de permissões do objeto, tem uma única função atribuída a ele.  
  
## <a name="role-and-role-member-objects"></a>Objetos da função e de membro da função  
 Uma função é um objeto contendo um conjunto de usuários (membros). Uma definição de função estabelece a associação dos usuários no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Como as permissões são atribuídas por função, um usuário deve ser um membro de uma função antes de acessar qualquer objeto.  
  
 Um <xref:Microsoft.AnalysisServices.Role> objeto é composto dos parâmetros Nome, ID e Membros. Os membros são um conjunto de cadeia de caracteres. Cada membro contém o nome do usuário na forma "domínio\nomedousuário." O nome é uma cadeia de caracteres que contém o nome da função. O ID é uma cadeia de caracteres que contém o identificador exclusivo da função.  
  
### <a name="server-role"></a>Função do servidor  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] função de servidor define o acesso administrativo de usuários do Windows e grupos a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Os membros dessa função têm acesso a todos os [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] bancos de dados e objetos em uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e pode executar as seguintes tarefas:  
  
-   Executar funções administrativas no nível do servidor, usando o SQL Server Management Studio ou o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], incluindo a criação de bancos de dados e propriedades no nível do servidor de configuração.  
  
-   Execute funções administrativas programaticamente com o AMO (Objetos de Gerenciamento de Análise).  
  
-   Manter funções de banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Iniciar os rastreamentos (diferentes dos para processar eventos, que podem ser executados por uma função de banco de dados com acesso Processo).  
  
 Toda instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tem uma função de servidor, que define quais usuários podem gerenciar aquela instância. O nome e ID dessa função é Administrators e, diferentemente de funções de bancos de dados, a função do servidor não pode ser excluída, nem permissões podem ser adicionadas ou removidas. Em outras palavras, um usuário é ou não é um administrador para uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], dependendo se ele ou ela está incluída na função de servidor para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="database-roles"></a>Funções de banco de dados  
 Uma [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] função de banco de dados define acesso do usuário a objetos e dados em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados. Uma função de banco de dados é criada como um objeto separado em um banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e aplica-se apenas ao banco de dados no qual a função foi criada. Os usuários e grupos do Windows são incluídos na função por um administrador que também define as permissões dentro da função.  
  
 As permissões de uma função podem permitir que os membros acessem e administrem o banco de dados, além de objetos e dados no banco de dados. Cada permissão tem um ou mais direitos de acesso associados a ele, os quais, por sua vez, dão à permissão um controle mais preciso sobre o acesso a um determinado objeto no banco de dados.  
  
## <a name="permission-objects"></a>Objetos de permissão  
 As permissões estão associadas a um objeto (cubo, dimensão, outros) para uma determinada função. As permissões especificam quais operações o membro da função pode executar no objeto.  
  
 A classe <xref:Microsoft.AnalysisServices.Permission> é uma classe abstrata. Portanto, você deve usar as classes derivadas para definir permissões para os objetos correspondentes. Para cada objeto, é definida uma classe derivada da permissão.  
  
|Object|Classe|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 As ações possíveis habilitadas por permissões são mostradas na lista:  
  
|Ação|Valores|Explicação|  
|------------|------------|-----------------|  
|Processar|{`true`, `false`}<br /><br /> Padrão=`false`|Se `true`, os membros podem processar o objeto e qualquer objeto contido no objeto.<br /><br /> As permissões de processo não se aplicam aos modelos de mineração. <xref:Microsoft.AnalysisServices.MiningModel> permissões são sempre herdadas de <xref:Microsoft.AnalysisServices.MiningStructure>.|  
|ReadDefinition|{`None`, `Basic`, `Allowed`}<br /><br /> Padrão=`None`|Especifica se membros podem ler a definição de dados (ASSL) associada ao objeto.<br /><br /> Se `Allowed`, os membros podem ler o ASSL associado ao objeto.<br /><br /> `Basic` e `Allowed` são herdadas pelos objetos que estão contidos no objeto. `Allowed` substitui `Basic` e `None`.<br /><br /> `Allowed` é necessário para DISCOVER_XML_METADATA em um objeto. `Basic` é necessário para criar objetos vinculados e cubos locais.|  
|leitura|{`None`, `Allowed`}<br /><br /> Padrão =`None` (exceto para DimensionPermission, onde padrão =`Allowed`)|Especifica se membros têm acesso de leitura a conjuntos de linhas do esquema e conteúdo de dados.<br /><br /> `Allowed` concede acesso de leitura em um banco de dados, que permite que você descubra um banco de dados.<br /><br /> `Allowed` em um cubo concede acesso de leitura nos conjuntos de linhas do esquema e acesso ao conteúdo do cubo (a menos que restringido por <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.CubeDimensionPermission>).<br /><br /> `Allowed` em uma dimensão concede permissão de leitura em todos os atributos na dimensão (a menos que restringidos por <xref:Microsoft.AnalysisServices.CubeDimensionPermission>). A permissão de leitura é usada para herança estática para o <xref:Microsoft.AnalysisServices.CubeDimensionPermission>. `None` em uma dimensão oculta a dimensão e concede acesso ao membro padrão apenas para atributos agregáveis; ocorrerá um erro se a dimensão contiver um atributo não agregável.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningModelPermission> concede permissões de visualização de objetos em conjuntos de linhas de esquema e executar associações previsíveis.<br /><br /> **NoteAllowed** é necessária para ler ou gravar em qualquer objeto no banco de dados.|  
|Gravação|{`None`, `Allowed`}<br /><br /> Padrão=`None`|Especifica se membros têm acesso de gravação aos dados do objeto pai.<br /><br /> O acesso aplica-se às subclasses <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube> e <xref:Microsoft.AnalysisServices.MiningModel>. Não se aplica ao banco de dados <xref:Microsoft.AnalysisServices.MiningStructure> subclasses, que gera um erro de validação.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.Dimension> concede permissão de gravação em todos os atributos na dimensão.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.Cube> concede permissão de gravação nas células do cubo para partições definidas como Type=write-back.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningModel> concede permissão para modificar o conteúdo modelo.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningStructure> não tem nenhum significado específico [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. **Observação:** gravação não pode ser definida como `Allowed` , a menos que uma leitura também é definida como `Allowed`|  
|Administrar **Observação:** somente nas permissões de banco de dados|{`true`, `false`}<br /><br /> Padrão=`false`|Especifica se membros podem administrar um banco de dados.<br /><br /> `true` concede aos membros acesso a todos os objetos em um banco de dados.<br /><br /> Um membro pode ter permissões Administrador para um banco de dados específico, mas não para outros.|  
  
## <a name="see-also"></a>Consulte também  
 [Autorizar o acesso a objetos e operações de &#40;Analysis Services&#41;](../authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
