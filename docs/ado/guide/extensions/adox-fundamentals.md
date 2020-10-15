---
description: Conceitos básicos do ADOX
title: Conceitos básicos do ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bb64cb60584444ba845ef1464fb07886c5db782
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098625"
---
# <a name="adox-fundamentals"></a>Conceitos básicos do ADOX
O Microsoft® ActiveX® extensões de objetos de dados para segurança e linguagem de definição de dados (ADOX) é uma extensão para os objetos ADO e o modelo de programação. O ADOX inclui objetos para a criação e modificação de esquemas, bem como segurança. Como é uma abordagem baseada em objeto para a manipulação de esquema, você pode escrever código que funcionará em várias fontes de dados, independentemente das diferenças em suas sintaxes nativas.  
  
 O ADOX é uma biblioteca complementar para os principais objetos do ADO. Ele expõe objetos adicionais para criar, modificar e excluir objetos de esquema, como tabelas e procedimentos. Ele também inclui objetos de segurança para manter usuários e grupos e conceder e revogar permissões em objetos.  
  
 Para usar o ADOX com sua ferramenta de desenvolvimento, você deve estabelecer uma referência à biblioteca de tipos do ADOX. A descrição da biblioteca do ADOX é "Microsoft ADO ext. para DDL e segurança". O nome do arquivo da biblioteca ADOX é Msadox.dll e a ID do programa (ProgID) é "ADOX". Para obter mais informações sobre como estabelecer referências a bibliotecas, consulte a documentação da sua ferramenta de desenvolvimento.  
  
 O provedor Microsoft OLE DB para o Microsoft Jet Mecanismo de Banco de Dados dá suporte total a ADOX. Alguns recursos do ADOX podem não ter suporte, dependendo do seu provedor de dados.  
  
 Este documento pressupõe um conhecimento prático da linguagem de programação Microsoft® Visual Basic® e um conhecimento geral do ADO. Para obter mais informações sobre o ADO, consulte o [Guia do programador do ADO](../ado-programmer-s-guide.md). Para obter mais informações gerais sobre o ADOX, consulte os seguintes tópicos:  
  
-   [Modelo de objeto ADOX](../../reference/adox-api/adox-object-model.md)  
  
-   [Objetos ADOX](../../reference/adox-api/adox-objects.md)  
  
-   [Coleções ADOX](../../reference/adox-api/adox-collections.md)  
  
-   [Propriedades ADOX](../../reference/adox-api/adox-properties.md)  
  
-   [Métodos do ADOX](../../reference/adox-api/adox-methods.md)  
  
-   [Exemplos do ADOX](../../reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADOX](../../reference/adox-api/adox-object-model.md?view=sql-server-ver15)   
 [Exemplos de código do ADOX](../../reference/adox-api/adox-code-examples.md)   
 [Coleções do ADOX](../../reference/adox-api/adox-collections.md)   
 [Constantes enumeradas do ADOX](../../reference/adox-api/adox-enumerated-constants.md)   
 [Métodos ADOX](../../reference/adox-api/adox-methods.md)   
 [Modelo de objeto ADOX](../../reference/adox-api/adox-object-model.md)   
 [Objetos ADOX](../../reference/adox-api/adox-objects.md)   
 [Propriedades do ADOX](../../reference/adox-api/adox-properties.md)   
 [ADO (Multidimensional) (ADO MD)](../multidimensional/ado-multidimensional-ado-md.md)   
 [Guia do programador do ADO](../ado-programmer-s-guide.md)
