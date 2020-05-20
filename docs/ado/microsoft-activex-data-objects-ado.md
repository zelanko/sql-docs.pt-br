---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18b9a6590ce777402456c8e9f8c8f28807ec5670
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606608"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ADO (ActiveX Data Objects)

ActiveX Data Objects é um modelo de programação, o que significa que ele não depende de nenhum mecanismo de back-end específico. Atualmente, no entanto, o único mecanismo que dá suporte ao modelo ADO é OLE-DB. Há muitos provedores OLE-DB nativos, bem como um provedor OLE-DB para ODBC. O ADO é usado em C++ e Visual Basic programas para se conectar a SQL Server e a outros bancos de dados. É claro que também funciona para se conectar ao banco de dados SQL do Azure na nuvem.

Cada seção neste artigo descreve um componente do ADO.

> [!NOTE]
> ADO.NET é diferente do ADO. ADO.NET e muitos outros drivers de conexão SQL e seus idiomas são discutidos a partir de [SQL Server drivers](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 O Microsoft ActiveX Data Objects (ADO) permite que seus aplicativos cliente acessem e manipulem dados de uma variedade de fontes por meio de um provedor de OLE DB. Seus principais benefícios são a facilidade de uso, a alta velocidade, a baixa sobrecarga de memória e uma pequena superfície de disco. O ADO oferece suporte aos principais recursos para a criação de aplicativos cliente/servidor e baseados na Web.  
  
## <a name="ado-md"></a>ADO MD  
 O Microsoft ActiveX Data Objects (Multidimensional) (ADO MD) fornece acesso fácil a dados multidimensionais de linguagens como Microsoft Visual Basic e Microsoft Visual C++. ADO MD estende o Microsoft ActiveX Data Objects (ADO) para incluir objetos específicos de dados multidimensionais, como os objetos CubeDef e células. Com ADO MD você pode procurar o esquema multidimensional, consultar um cubo e recuperar os resultados.  
  
 Assim como o ADO, o ADO MD usa um provedor de OLE DB subjacente para obter acesso aos dados. Para trabalhar com ADO MD, o provedor deve ser um MDP (provedor de dados multidimensional), conforme definido pelo OLE DB para especificação de OLAP. MDPs apresentam dados em exibições multidimensionais em vez de TDPs (provedores de dados de tabela) que apresentam dados em exibições de tabela. Consulte a documentação do seu provedor de OLE DB OLAP para obter informações mais detalhadas sobre a sintaxe e os comportamentos específicos com suporte no seu provedor.  
  
## <a name="rds"></a>RDS  
 O RDS (serviço de dados remotos) é um recurso do ADO, com o qual você pode mover dados de um servidor para um aplicativo cliente ou página da Web, manipular os dados no cliente e retornar atualizações para o servidor em uma única viagem de ida e volta.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 O Microsoft ActiveX Data Objects Extensions para segurança e linguagem de definição de dados (ADOX) é uma extensão para os objetos ADO e o modelo de programação. O ADOX inclui objetos para a criação e modificação de esquemas, bem como segurança. Como é uma abordagem baseada em objeto para a manipulação de esquema, você pode escrever código que funcionará em várias fontes de dados, independentemente das diferenças em suas sintaxes nativas.  
  
 O ADOX é uma biblioteca complementar para os principais objetos do ADO. Ele expõe objetos adicionais para criar, modificar e excluir objetos de esquema, como tabelas e procedimentos. Ele também inclui objetos de segurança para manter usuários e grupos e conceder e revogar permissões em objetos.  
  
## <a name="documentation"></a>Documentação  
 [Problemas de design de segurança ADO](../ado/guide/ado-security-design-issues.md)  
  
 [Guia do programador do ADO](../ado/guide/ado-programmer-s-guide.md)  
  
 Uma introdução ao uso do ADO, do RDS, do ADO MD e do ADOX.  
  
 [Referência do programador do ADO](../ado/reference/ado-programmer-s-reference.md)  
  
 Esta seção da documentação do ADO contém tópicos para cada objeto ADO, RDS, ADO MD e ADOX, coleção, propriedade, propriedade dinâmica, método, evento e enumeração.  
  
 [Glossário ADO](../ado/ado-glossary.md)  
  
## <a name="support"></a>Suporte  
 Para obter ajuda gratuita com problemas do ADO, tente postar no grupo de notícias público do ADO. Este grupo de notícias é monitorado pelos profissionais de suporte do PSS (Atendimento Microsoft) que abordam o ADO e por outros desenvolvedores experientes do ADO.  
  
 Mais informações sobre as opções de suporte podem ser encontradas no site de ajuda e suporte da Microsoft.


