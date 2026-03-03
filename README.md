content').forEach(c => c.classList.remove('active'));
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        document.getElementById('content-'+i).classList.add('active');
        document.querySelectorAll('.tab')[i-1].classList.add('active');
    };

    function showToast(m) { var x = document.getElementById("toast"); x.className="show"; x.innerText=m; setTimeout(()=>x.className=x.className.replace("show",""),3000); }
    window.initCodeDropdown();
</script>
</body>
</html>