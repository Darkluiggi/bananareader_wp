<template>
  <input type="button" value="SOAP Request" @click="soapRequest();" />
</template>

<script>
export default {
  name: "SOAPIndex",
  data() {
    return {
      user: "",
    };
  },
  methods: {
    soapRequest() {
      // eslint-disable-next-line no-debugger
      debugger
      var str =
        '<?xml version="1.0" encoding="UTF-8"?>' +
        '<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">' +
        "<soap:Header/>" +
        "<soap:Body>" +
        "<tem:DocumentsRequest>" +
        "<tem:user>3</tem:user>" +
        "</tem:DocumentsRequest>" +
        "</soap:Body>" +
        "</soap:Envelope>";

      var xhr = this.createCORSRequest(
        "POST",
        "http://35.239.72.193:3002/wsdl?wsdl"
      );
      if (!xhr) {
        console.log("XHR issue");
        return;
      }

      xhr.onload = function() {
        const array = [];
        var results = xhr.responseText;
        console.log(results);

        for (const [documents_user] of Object.entries(results)) {
          array.push([documents_user]);
        }
        console.log(array);
      };

      xhr.setRequestHeader("Content-Type", "text/xml");
      xhr.send(str);
    },
    createCORSRequest(method, url) {
      var xhr = new XMLHttpRequest();
      if ("withCredentials" in xhr) {
        xhr.open(method, url, false);
      } else if (typeof XDomainRequest != "undefined") {
        alert;
        // eslint-disable-next-line no-undef
        xhr = new XDomainRequest();
        xhr.open(method, url);
      } else {
        console.log("CORS not supported");
        alert("CORS not supported");
        xhr = null;
      }
      return xhr;
    },
  },

  mounted() {},
};
</script>

<style></style>
