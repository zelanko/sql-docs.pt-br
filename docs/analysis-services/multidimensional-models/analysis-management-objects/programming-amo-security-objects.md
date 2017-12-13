---
title: "Programação de objetos de segurança AMO | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d8733a0255c22701009baf79892d7ff6f83b9c87
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="programming-amo-security-objects"></a>Programando objetos de segurança AMO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], programação de objetos de segurança ou executar aplicativos que usam objetos de segurança AMO exige um membro do grupo administrador do servidor ou o grupo de administradores de banco de dados. Administrador de servidor e administrador de banco de dados são um acesso níveis fornecido pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 No [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], o acesso de usuário a qualquer objeto é obtido pela combinação de Funções e Permissões atribuídas àquele objeto. Para obter mais informações, consulte [Classes de segurança AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md).  
  
## <a name="role-and-permission-objects"></a>Objetos de função e de permissão  
 As funções de servidor contêm somente uma função na coleção, Administradores. Não é possível adicionar novas funções à coleção de funções de servidor. A associação à função Administradores permite acesso completo a todos os objeto do servidor  
  
 Os objetos de <xref:Microsoft.AnalysisServices.Role> são criados no banco de dados. A manutenção de funções só requer a adição ou remoção de membros da função e a adição ou descarte de funções no objeto <xref:Microsoft.AnalysisServices.Database>. Uma função não poderá ser descartada se qualquer objeto <xref:Microsoft.AnalysisServices.Permission> estiver associado a ela. Para descartar uma função, todos os objetos de <xref:Microsoft.AnalysisServices.Permission> nos objetos <xref:Microsoft.AnalysisServices.Database> deverão ser pesquisados e <xref:Microsoft.AnalysisServices.Role> deverá ser removido das permissões, antes que <xref:Microsoft.AnalysisServices.Role> possa ser descartado de <xref:Microsoft.AnalysisServices.Database>.  
  
 As permissões definem as ações habilitadas no objeto onde a permissão foi fornecida. Podem ser fornecidas permissões para os seguintes objetos: <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure>e <xref:Microsoft.AnalysisServices.MiningModel>. A manutenção da permissão envolve concessão ou revogação o acesso habilitado pela propriedade de acesso correspondente. Para cada acesso habilitado, existe uma propriedade que pode ser definida com o nível desejado de acesso. O acesso pode ser definido para as seguintes operações: Processo, ReadDefinition, Leitura, Gravação e Administrar. O acesso de administração só será definido no objeto <xref:Microsoft.AnalysisServices.Database>. O nível de segurança de administrador de banco de dados é obtido quando a função é concedida com a permissão de banco de dados Administer.  
  
 O exemplo a seguir cria quatro funções: Administradores de Banco de Dados, Processadores, Gravadores e Leitores.  
  
 Os Administradores de Banco de Dados podem administrar o banco de dados fornecido.  
  
 Os Processadores podem processar todos os objetos de um banco de dados e verificar os resultados. Para verificar os resultados, o acesso de leitura ao objeto de banco de dados deve ser explicitamente habilitado no cubo fornecido, já que a permissão de leitura não se aplica a objetos filhos.  
  
 Os Gravadores podem ler o cubo fornecido e podem gravar nele, e o acesso de célula está limitado a 'Estados Unidos' na dimensão de cliente.  
  
 Os Leitores podem ler o cubo fornecido e o acesso de célula está limitado a 'Estados Unidos' na dimensão de cliente.  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programando objetos de segurança AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [Permissões e direitos de acesso &#40; Analysis Services - dados multidimensionais &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
