---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12db230262927ce93abeb1955c8ab7834db953f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO é usado em programas C++ para se conectar ao SQL Server. Naturalmente, também funciona para se conectar ao banco de dados SQL Azure na nuvem.

Cada seção deste artigo descreve um componente do ADO.

> [!NOTE]
> O ADO.NET é diferente do ADO. ADO.NET e muitos outros drivers de conexão SQL e suas linguagens, são discutidas começando em [Drivers do SQL Server](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) permitem que os aplicativos de cliente acessar e manipular dados de uma variedade de fontes por meio de um provedor OLE DB. Seus principais benefícios são a facilidade de uso, de alta velocidade, baixa sobrecarga da memória e um espaço pequeno disco. ADO dá suporte a recursos importantes para a criação de cliente/servidor e aplicativos baseados na Web.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (Multidimensional) (ADO MD) oferece acesso fácil a dados multidimensionais de linguagens, como Microsoft Visual Basic e Microsoft Visual C++. ADO MD estende Microsoft ActiveX Data Objects (ADO) para incluir objetos específicos para dados multidimensionais, como os objetos CubeDef e o conjunto de células. Com ADO MD procurar esquema multidimensional, um cubo de consulta e recuperar os resultados.  
  
 Como ADO, o ADO MD usa um provedor OLE DB subjacente para obter acesso aos dados. Para trabalhar com ADO MD, o provedor deve ser um provedor de dados multidimensional (MDP) conforme definido pelo OLE DB para a especificação OLAP. MDPs apresentar dados nos modos de exibição multidimensionais em vez de provedores de dados de tabela (TDPs) os dados presentes nos modos de exibição tabulares. Consulte a documentação para o seu provedor de OLE DB OLAP para obter mais informações sobre a sintaxe específica e comportamentos suportados pelo provedor.  
  
## <a name="rds"></a>RDS  
 Remote Data Service (RDS) é um recurso do ADO, com a qual você pode mover dados de um servidor para um aplicativo cliente ou página da Web, manipular os dados no cliente e retornar as atualizações para o servidor em uma única viagem de ida.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 Objetos do Microsoft ActiveX dados extensões de linguagem de definição de dados e de segurança (ADOX) é uma extensão para os objetos do ADO e o modelo de programação. ADOX inclui objetos para criação de esquema e modificação, bem como a segurança. Como é uma abordagem baseada em objeto para manipulação de esquema, você pode escrever código que funciona em dados de várias fontes, independentemente das diferenças nas suas sintaxes nativo.  
  
 ADOX é uma biblioteca de complementar para os objetos principais do ADO. Expõe objetos adicionais para criar, modificar e excluir objetos de esquema, como tabelas e procedimentos. Ele também inclui objetos de segurança para manter usuários e grupos e para conceder e revogar permissões em objetos.  
  
## <a name="documentation"></a>Documentação  
 [Problemas de design de segurança ADO](../ado/guide/ado-security-design-issues.md)  
  
 [Guia do programador do ADO](../ado/guide/ado-programmer-s-guide.md)  
  
 Uma introdução ao uso de ADO, RDS, ADO MD e ADOX.  
  
 [Referência do programador do ADO](../ado/reference/ado-programmer-s-reference.md)  
  
 Esta seção da documentação do ADO contém tópicos para cada ADO, RDS, ADO MD e ADOX objeto, coleção, propriedade, propriedades dinâmicas, método, eventos e enumeração.  
  
 [Glossário ADO](../ado/ado-glossary.md)  
  
## <a name="support"></a>Suporte  
 Livre ajuda com problemas de ADO, tente lançamento para o grupo de notícias público do ADO. Este grupo de notícias é monitorado por profissionais de suporte do Microsoft Product Support Services (PSS) que abrangem o ADO e por outros desenvolvedores experientes do ADO.  
  
 Mais informações sobre opções de suporte podem ser encontradas no site do Microsoft Help e suporte da.


