using System;
using System.Configuration;

namespace TestAsmxProject.Filter.HTTP
{
    [AttributeUsage(AttributeTargets.Method, Inherited = true, AllowMultiple = false)]
    public sealed class IpFilterAttribute : Attribute
    {
        public string[] AllowedIps { get; private set; }

        public IpFilterAttribute(params string[] ips)
        {
            string configIps = ConfigurationManager.AppSettings["IpWhiteList"];
            var configAllowedIps = !string.IsNullOrEmpty(configIps)
                ? configIps.Split(new[] { ',' }, StringSplitOptions.RemoveEmptyEntries)
                : new string[] { };
            AllowedIps = new string[ips.Length + configAllowedIps.Length];
            ips.CopyTo(AllowedIps, 0);
            configAllowedIps.CopyTo(AllowedIps, ips.Length);
        }

        public bool IsAllowedIp(string userIp)
        {
            return AllowedIps.Any(ip => userIp == ip);
        }
    }
}
