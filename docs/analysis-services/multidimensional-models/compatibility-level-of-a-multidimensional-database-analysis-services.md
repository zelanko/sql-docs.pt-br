---
title: "Nível de compatibilidade de um banco de dados Multidimensional (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 978279e6-a581-4184-af9d-8701b9826a89
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f408b0bb6b2b0fbed6b53046f6ce6e70adb49040
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="compatibility-level-of-a-multidimensional-database-analysis-services"></a>Nível de compatibilidade de um banco de dados multidimensional (Analysis Services)
  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a propriedade de nível de compatibilidade do banco de dados determina o nível funcional de um banco de dados. Os níveis de compatibilidade são exclusivos de cada tipo de modelo. Por exemplo, um nível de compatibilidade **1100** tem um significado diferente quando o banco de dados é multidimensional ou tabular.  
  
 Este tópico descreve o nível de compatibilidade apenas para bancos de dados multidimensionais. Para obter mais informações sobre soluções tabulares, consulte [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
> [!NOTE]  
>  Os modelos de tabela têm níveis adicionais de compatibilidade de banco de dados que não se aplicam a modelos multidimensionais. O nível de compatibilidade **1103** não existe para os modelos multidimensionais. Consulte [What is new for the Tabular model in SQL Server 2012 SP1 and compatibility level](http://go.microsoft.com/fwlink/?LinkId=301727) [Novidades no modelo Tabular no SQL Server 2012 SP1 e nível de compatibilidade] para obter mais informações sobre o nível **1103** para soluções tabulares.  
  
 **Níveis de compatibilidade para bancos de dados multidimensionais**  
  
 No momento, o único comportamento do banco de dados multidimensional que varia de acordo com o nível funcional é a arquitetura de armazenamento de cadeia de caracteres. Ao aumentar o nível de compatibilidade do banco de dados, você pode substituir o limite máximo de 4 gigabytes para o armazenamento de cadeia de caracteres de medidas e dimensões.  
  
 Para um banco de dados multidimensional, os valores válidos para a propriedade **CompatibilityLevel** incluem o seguinte:  
  
|Configuração|Description|  
|-------------|-----------------|  
|**1050**|Este valor não é visível em script ou em ferramentas, mas ele corresponde a bancos de dados criados no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]ou no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Qualquer banco de dados que não tenha **CompatibilityLevel** definido explicitamente será executado implicitamente no nível **1050** .|  
|**1100**|Este é o valor padrão para novos bancos de dados criados no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Você também pode especificá-lo para bancos de dados criados em versões anteriores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para habilitar o uso de recursos com suporte apenas neste nível de compatibilidade (isto é, aumento no armazenamento de cadeia de caracteres para atributos de dimensão ou medidas de contagens distintas que contêm dados de cadeia de caracteres).<br /><br /> Os bancos de dados com o **CompatibilityLevel** definido como **1100** obtêm uma propriedade adicional, **StringStoresCompatibilityLevel**, a qual permite escolher um armazenamento de cadeia de caracteres alternativo para partições e dimensões.|  
  
> [!WARNING]  
>  A definição da compatibilidade do banco de dados como um nível mais alto é irreversível. Após aumentar o nível de compatibilidade para **1100**, você deve continuar executando o banco de dados em servidores mais recentes. Não é possível reverter para **1050**. Você não pode anexar nem restaurar um banco de dados **1100** em uma versão de servidor anterior ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Os níveis de compatibilidade do banco de dados são apresentados no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Você precisa ter um [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou superior para exibir ou definir o nível de compatibilidade do banco de dados.  
  
 O banco de dados não pode ser um cubo local. Os cubos locais não dão suporte à propriedade **CompatibilityLevel** .  
  
 O banco de dados deve ter sido criado em uma versão anterior (SQL Server 2008 R2 ou anterior) e, depois, anexado ou restaurado para um servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou superior. Os bancos de dados implantados no SQL Server 2012 já estão em **1100** e não podem ser rebaixados para execução em um nível inferior.  
  
## <a name="determine-the-existing-database-compatibility-level-for-a-multidimensional-database"></a>Como determinar o nível de compatibilidade do banco de dados existente para um banco de dados multidimensional  
 A única maneira de exibir ou modificar o nível de compatibilidade do banco de dados é através do XMLA. Você pode exibir ou modificar o script XMLA que especifica o banco de dados no SQL Server Management Studio.  
  
 Caso você pesquise a definição XMLA de um banco de dados para a propriedade **CompatibilityLevel** e ela não exista, é mais provável que você tenha um banco de dados no nível **1050** .  
  
 Instruções para exibir e modificar o script XMLA são fornecidas na próxima seção.  
  
## <a name="set-the-database-compatibility-level-in-sql-server-management-studio"></a>Como definir o nível de compatibilidade do banco de dados no SQL Server Management Studio  
  
1.  Antes de elevar o nível de compatibilidade, faça o backup do banco de dados caso queira reverter posteriormente as alterações.  
  
2.  Usando o SQL Server Management Studio, conecte-se ao servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que hospeda o banco de dados.  
  
3.  Clique com o botão direito do mouse no nome do banco de dados, aponte para **Script de Banco de Dados como**, aponte para **ALTER para**e selecione **Janela do Editor de Nova Consulta**. Uma representação XMLA do banco de dados será aberta em uma nova janela.  
  
4.  Copie o seguinte elemento XML:  
  
    ```  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    ```  
  
5.  Cole-o após o elemento de fechamento `</Annotations>` e antes do elemento `<Language>` . O XML deve ter aparência semelhante ao seguinte exemplo:  
  
    ```  
    </Annotations>  
    <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
    <Language>1033</Language>  
    ```  
  
6.  Salve o arquivo.  
  
7.  Para executar o script, clique em **Executar** no menu Consulta ou pressione F5.  
  
## <a name="supported-operations-that-require-the-same-compatibility-level"></a>Operações suportadas que exigem o mesmo nível de compatibilidade  
 As operações a seguir exigem que os bancos de dados de origem compartilhem o mesmo nível de compatibilidade.  
  
1.  Há suporte à mesclagem de partições de diferentes bancos de dados somente quando os dois bancos de dados compartilham o mesmo nível de compatibilidade.  
  
2.  O uso de dimensões vinculadas de outro banco de dados requer o mesmo nível de compatibilidade. Por exemplo, se você quiser usar uma dimensão vinculada de um banco de dados [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] em um banco de dados [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , você deverá compatibilizar o banco de dados [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] para um servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e definir o nível de compatibilidade como **1100**.  
  
3.  A sincronização de servidores tem suporte apenas para servidores que compartilham a mesma versão e o mesmo nível de compatibilidade de banco de dados.  
  
## <a name="next-steps"></a>Próximas etapas  
 Após aumentar o nível de compatibilidade do banco de dados, você pode definir a propriedade **StringStoresCompatibilityLevel** no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Isso aumenta o armazenamento de cadeia de caracteres para medidas e dimensões. Para obter mais informações sobre esse recurso, consulte [Configurar o armazenamento de cadeia de caracteres para dimensões e partições](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
