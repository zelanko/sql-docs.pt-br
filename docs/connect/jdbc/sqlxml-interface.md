---
title: Interface SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6257f3575412bc35b00722a0b5da6b8c5ca74f10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815994"
---
# <a name="sqlxml-interface"></a>Interface SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O driver JDBC fornece suporte para a API do JDBC 4.0, que apresenta a interface java.sql.SQLXML. A interface SQLXML define métodos para interagir com os dados XML e manipulá-los. O **SQLXML** tipo de dados é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml** tipo de dados.  
  
A interface SQLXML fornece métodos para acessar o valor XML como uma **cadeia de caracteres**, um **leitor** ou **gravador**, ou como um **Stream**. O valor XML também pode ser acessado por meio de uma **Fonte** ou definido como um **Resultado**, que é usado com APIs do Analisador de XML como DOM (Modelo de Objeto do Documento), SAX (API Simples para XML) e StAX (API de Fluxo para XML), assim como transformações XSLT e XPath.  
  
## <a name="remarks"></a>Remarks  

A tabela a seguir descreve os métodos definidos na interface SQLXML:  
  
|Sintaxe de método|Descrição de método|  
|-------------------|------------------------|  
|[void free()](http://go.microsoft.com/fwlink/?LinkId=131685)|Esse método libera o objeto SQLXML e os recursos que ele contém.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|Retorna um fluxo de entrada para ler dados do SQLXML.|  
|[Reader getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|Retorna os dados **XML** como um objeto java.io.Reader ou como um fluxo de caracteres.|  
|[T estende o código-fonte T getSource (classe\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|Retorna um **fonte** para ler o **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Observação:** o método getSource é compatível com as seguintes origens: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource e java.io.InputStream.|  
|[String getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|Retorna uma representação de cadeia de caracteres do valor **XML** designado por este objeto SQLXML.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|Recupera um fluxo que pode ser usado para gravar o valor **XML** que este objeto SQLXML representa.|  
|[Writer setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|Retorna um fluxo para ser usado para gravar o valor **XML** que este objeto SQLXML representa.|  
|[Estende o T T resultado setResult (classe\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|Retorna um **resultado** para a configuração do **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Observação:** o método setResult é compatível com as seguintes origens: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult e java.io.OutputStream.|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|Define o valor XML designado por esse objeto SQLXML para a representação **String** especificada.|  
  
Os aplicativos podem ler e gravar valores XML para ou de um objeto SQLXML apenas uma vez.  
  
Quando o método free() é chamado, um objeto SQLXML se torna inválido e não é nem legível nem gravável. Se o aplicativo tentar invocar um método naquele objeto SQLXML diferente do método free(), uma exceção será lançada.  
  
O objeto SQLXML não fica legível nem gravável quando o aplicativo chama qualquer um dos seguintes métodos de getter: getSource, getCharacterStream, getBinaryStream e getString.  
  
O objeto SQLXML se torna nem legível nem gravável quando o aplicativo chama qualquer um dos seguintes métodos de setter: setResult, setCharacterStream, setBinaryStream e setString.  
  
## <a name="see-also"></a>Consulte Também  

[Dando suporte a dados XML](../../connect/jdbc/supporting-xml-data.md)  
