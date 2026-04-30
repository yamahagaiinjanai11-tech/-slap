#slapSound.currentTime = 0;
        slapSound.play();

        // 視覚エフェクト
        target.classList.add('slap-effect');
        setTimeout(() => {
            target.classList.remove('slap-effect');
        }, 100);

        // 少しランダムに跳ねる動き
        const randomX = (Math.random() - 0.5) * 20;
        const randomY = (Math.random() - 0.5) * 20;
        target.style.transform = `translate(${randomX}px, ${randomY}px)`;
    }
</script>

</body>
</html>

        