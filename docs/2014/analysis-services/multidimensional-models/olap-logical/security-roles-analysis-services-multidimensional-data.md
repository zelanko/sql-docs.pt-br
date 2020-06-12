---
title: Funções de segurança (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: e62abaab5a8f74dfee7d51962f2fb243dc6eb20a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545988"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>Funções de Segurança (Analysis Services - Dados Multidimensionais)
  As funções são usadas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para gerenciar a segurança de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos e dados. Em termos básicos, uma função associa os identificadores de segurança (SIDs) dos usuários e grupos do Microsoft Windows que têm direitos de acesso e permissões específicas para objetos gerenciados por uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Dois tipos de funções são fornecidos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:  
  
-   A função do servidor, uma função fixa que fornece acesso de administrador a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   As funções de banco de dados, funções definidas por administradores para controlar o acesso a objetos e dados para usuários não administradores.  
  
 A segurança na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] segurança é gerenciada usando funções e permissões. As funções são grupos de usuários. Os usuários, também chamados de membros, podem ser adicionados ou removidos das funções. Permissões para objetos são especificadas por funções e todos os membros em uma função podem usar os objetos para o qual tem permissão. Todos os membros em uma função têm permissões iguais para os objetos. As permissões são específicas dos objetos. Cada objeto tem um conjunto de permissões concedidas para esse objeto; diferentes conjuntos de permissões podem ser concedidos para um objeto. Cada permissão, do conjunto de permissões do objeto, tem uma única função atribuída a ele.  
  
## <a name="role-and-role-member-objects"></a>Objetos da função e de membro da função  
 Uma função é um objeto contendo um conjunto de usuários (membros). Uma definição de Função estabelece a associação de usuários no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Como as permissões são atribuídas por função, um usuário deve ser um membro de uma função antes de acessar qualquer objeto.  
  
 Um <xref:Microsoft.AnalysisServices.Role> objeto é composto dos parâmetros Nome, ID e Membros. Os membros são um conjunto de cadeia de caracteres. Cada membro contém o nome do usuário na forma "domínio\nomedousuário." O nome é uma cadeia de caracteres que contém o nome da função. O ID é uma cadeia de caracteres que contém o identificador exclusivo da função.  
  
### <a name="server-role"></a>Função de servidor  
 A função de servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] define o acesso administrativo de usuários e grupos do Windows a uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Os membros dessa função têm acesso a todos os bancos de dados e objetos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e podem executar as seguintes tarefas:  
  
-   Executar funções administrativas no nível do servidor, usando o SQL Server Management Studio ou o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], incluindo a criação de bancos de dados e propriedades no nível do servidor de configuração.  
  
-   Execute funções administrativas programaticamente com o AMO (Objetos de Gerenciamento de Análise).  
  
-   Manter funções de banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   Iniciar os rastreamentos (diferentes dos para processar eventos, que podem ser executados por uma função de banco de dados com acesso Processo).  
  
 Toda instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tem uma função de servidor, que define quais usuários podem gerenciar aquela instância. O nome e ID dessa função é Administrators e, diferentemente de funções de bancos de dados, a função do servidor não pode ser excluída, nem permissões podem ser adicionadas ou removidas. Em outras palavras, um usuário é ou não é um administrador de uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], dependendo o usuário está incluído na função de servidor para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="database-roles"></a>Funções de banco de dados  
 Uma função de banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] define o acesso do usuário a objetos e dados em um banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Uma função de banco de dados é criada como um objeto separado em um banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e aplica-se apenas ao banco de dados no qual a função foi criada. Os usuários e grupos do Windows são incluídos na função por um administrador que também define as permissões dentro da função.  
  
 As permissões de uma função podem permitir que os membros acessem e administrem o banco de dados, além de objetos e dados no banco de dados. Cada permissão tem um ou mais direitos de acesso associados a ele, os quais, por sua vez, dão à permissão um controle mais preciso sobre o acesso a um determinado objeto no banco de dados.  
  
## <a name="permission-objects"></a>Objetos de permissão  
 As permissões estão associadas a um objeto (cubo, dimensão, outros) para uma determinada função. As permissões especificam quais operações o membro da função pode executar no objeto.  
  
 A classe <xref:Microsoft.AnalysisServices.Permission> é uma classe abstrata. Portanto, você deve usar as classes derivadas para definir permissões para os objetos correspondentes. Para cada objeto, é definida uma classe derivada da permissão.  
  
|Objeto|Classe|  
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
|Processar|{`true`, `false`}<br /><br /> Padrão=`false`|Se `true`, os membros podem processar o objeto e qualquer objeto contido no objeto.<br /><br /> As permissões de processo não se aplicam aos modelos de mineração. Permissões <xref:Microsoft.AnalysisServices.MiningModel> sempre são herdadas de <xref:Microsoft.AnalysisServices.MiningStructure>.|  
|ReadDefinition|{`None`, `Basic`, `Allowed`}<br /><br /> Padrão=`None`|Especifica se membros podem ler a definição de dados (ASSL) associada ao objeto.<br /><br /> Se `Allowed`, os membros podem ler o ASSL associado ao objeto.<br /><br /> `Basic` e `Allowed` são herdados por objetos contidos no objeto. `Allowed` substitui `Basic` e `None`.<br /><br /> `Allowed` é necessário para DISCOVER_XML_METADATA em um objeto. `Basic` é necessário para criar objetos vinculados e cubos locais.|  
|Ler|{`None`, `Allowed`}<br /><br /> Padrão =`None` (exceto para DimensionPermission, onde padrão=`Allowed`)|Especifica se membros têm acesso de leitura a conjuntos de linhas do esquema e conteúdo de dados.<br /><br /> `Allowed`fornece acesso de leitura em um banco de dados, que permite descobrir um banco de dados.<br /><br /> `Allowed` em um cubo concede acesso de leitura nos conjuntos de linhas do esquema e acesso ao conteúdo do cubo (a menos que restringido por <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.CubeDimensionPermission>).<br /><br /> `Allowed` em uma dimensão concede permissão de leitura em todos os atributos na dimensão (a menos que restringidos por <xref:Microsoft.AnalysisServices.CubeDimensionPermission>). A permissão de leitura é usada para herança estática para o <xref:Microsoft.AnalysisServices.CubeDimensionPermission>. `None` em uma dimensão oculta a dimensão e concede acesso ao membro padrão apenas para atributos agregáveis; ocorrerá um erro se a dimensão contiver um atributo não agregável.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningModelPermission> concede permissões de visualização de objetos em conjuntos de linhas de esquema e executar associações previsíveis.<br /><br /> **NoteAllowed** é necessário para ler ou gravar em qualquer objeto no banco de dados.|  
|Gravar|{`None`, `Allowed`}<br /><br /> Padrão=`None`|Especifica se membros têm acesso de gravação aos dados do objeto pai.<br /><br /> O acesso aplica-se às subclasses <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube> e <xref:Microsoft.AnalysisServices.MiningModel>. Ele não se aplica às subclasses de banco de dados <xref:Microsoft.AnalysisServices.MiningStructure> que geram um erro de validação.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.Dimension> concede permissão de gravação em todos os atributos na dimensão.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.Cube> concede permissão de gravação nas células do cubo para partições definidas como Type=write-back.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningModel> concede permissão para modificar o conteúdo modelo.<br /><br /> `Allowed` em um <xref:Microsoft.AnalysisServices.MiningStructure> não tem nenhum significado específico em [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. **Observação:**  A gravação não pode ser definida para a `Allowed` menos que Read também seja definido como`Allowed`|  
|Administrar **Observação:** somente nas permissões de banco de dados|{`true`, `false`}<br /><br /> Padrão=`false`|Especifica se membros podem administrar um banco de dados.<br /><br /> `true` concede acesso de membros a todos os objetos em um banco de dados.<br /><br /> Um membro pode ter permissões Administrador para um banco de dados específico, mas não para outros.|  
  
## <a name="see-also"></a>Consulte Também  
 [Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](../authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
