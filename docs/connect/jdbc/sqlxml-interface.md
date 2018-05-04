---
title: Interface SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed3d2dbac3ea244565e04046ec307b1386777efe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlxml-interface"></a>Interface SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O driver JDBC fornece suporte para a API do JDBC 4.0, que apresenta a interface java.sql.SQLXML. A interface SQLXML define métodos para interagir e manipular dados XML. O **SQLXML** tipo de dados mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de dados.  
  
 A interface SQLXML fornece métodos para acessar o valor XML como um **cadeia de caracteres**, um **leitor** ou **gravador**, ou como um **fluxo**. O valor XML também pode ser acessado por meio de um **fonte** ou definido como um **resultados**, que são usados com as APIs de analisador XML como modelo de objeto de documento (DOM), API simples para XML (SAX) e API de fluxo para XML (StAX), como bem como com o XSLT transforma e XPath.  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir descreve os métodos definidos na interface SQLXML:  
  
|Sintaxe de método|Descrição de método|  
|-------------------|------------------------|  
|[void free()](http://go.microsoft.com/fwlink/?LinkId=131685)|Esse método libera o objeto SQLXML e os recursos que ele contém.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|Retorna um fluxo de entrada para ler dados do SQLXML.|  
|[Leitor getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|Retorna o **XML** dados como um objeto Java.IO. Reader ou como um fluxo de caracteres.|  
|[T estende getSource fonte T (classe\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|Retorna um **fonte** para ler o **XML** valor especificado por esse **SQLXML** objeto.<br /><br /> **Observação:** o método getSource suporta as seguintes fontes: javax.XML.Transform.DOM, javax.xml.transform.sax.SAXSource, javax.XML e Java.IO. InputStream.|  
|[Cadeia de caracteres GetString)](http://go.microsoft.com/fwlink/?LinkId=131757)|Retorna uma representação de cadeia de caracteres da **XML** valor designado pelo objeto SQLXML.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|Recupera um fluxo que pode ser usado para gravar o **XML** valor que este objeto SQLXML representa.|  
|[Gravador setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|Retorna um fluxo a ser usado para gravar o **XML** valor que este objeto SQLXML representa.|  
|[T estende resultado T setResult (classe\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|Retorna um **resultados** para configuração de **XML** valor especificado por esse **SQLXML** objeto.<br /><br /> **Observação:** o método setResult suporta as seguintes fontes: javax.XML.Transform.DOM, javax.xml.transform.sax.SAXResult, javax.XML e OutputStream.|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|Define o valor XML designado por este objeto SQLXML especificado **cadeia de caracteres** representação.|  
  
 Os aplicativos podem ler e gravar valores XML para ou de um objeto SQLXML apenas uma vez.  
  
 Quando o método free() é chamado, um objeto SQLXML se torna inválido e não é legível nem gravável. Se o aplicativo tentar invocar um método naquele objeto SQLXML diferente do método free(), uma exceção será lançada.  
  
 O objeto SQLXML não fica legível nem gravável quando o aplicativo chama qualquer um dos seguintes métodos getter: getSource, getCharacterStream, getBinaryStream e getString.  
  
 O objeto SQLXML se torna nem legível nem gravável quando o aplicativo chama qualquer um dos seguintes métodos setter: setResult, setCharacterStream, setBinaryStream e setString.  
  
## <a name="see-also"></a>Consulte também  
 [Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)  
  
  
